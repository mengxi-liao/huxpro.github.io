---
layout:     post
title:      "ActiveRecord Optimization"
subtitle:   "Optimizing performance by using ActiveRecord properly"
date:       2018-02-17 12:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Ruby on Rails
---

> “Rails could be not that slow...”

![](/img/posts/active-record-optimization/slow-website.jpg)

## Better Rails: ActiveRecord Optimization

All web applications need to interact with databases and ActiveRecord makes it so easy. With the default .where and .save methods, we could easily retrieve and persist objects in a Rails application. It is simple and fast enough, for most of the cases.

But this is not true anymore when you aim to build a large application. In my team, our major application has a MySQL database with more than 100 tables and some tables have more than ten million objects. Some early code using ActiveRecord in a naive way significantly slow down some features and sometimes put our server on fire due to too much memory consumption. As a result, our team spends a lot of time in optimizing the ActiveRecord codes. It is very painful as the existing application is huge and bad codes are everywhere. It could be much easier if we paid more attention to performance when the app was built in draft.

This post aims to summarize the tips on how to use ActiveRecord in an optimized way. In fact, the secret is commonly known as follows: Fewer hits to the database, only retrieve the data needed and cache the data.

Before the actual tips, let’s define some models and associations as an example for future discussion. Let’s say we have an Article model and a Review model. Each article has a title field, a long content field and two timestamps created_at and updated_at. An article can have many reviews. Each review has article_id pointing to its article, a rating field from 1 to 5, a comment field and two timestamps created_at and updated_at.

## 1. Proper indexing

This is common sense. we all need an index. If there’s any feature needs to do review.article, ActiveRecord does a query like this:

SELECT "articles".* FROM "articles"
WHERE "articles"."id" = 2 ORDER BY "articles"."id" ASC LIMIT 1
If we don’t have an index on “articles”.”id”. The query will become slow significantly when the article table becomes huge. we could add an index to the attribute through migration.

```ruby
add_index :reviews, :article_id
```

## 2. Avoid N+1 queries problem for update/destroy.

When we need to manipulate a subset of objects, some developers like doing the following:

```ruby
@article.reviews.each do |r|
  r.destroy if r.comment.blank?
end
```

The problem with the above code is that it creates multiple queries in the database. If you check the server log, you will see something like this.

```SQL
SELECT "reviews".* FROM "reviews"
WHERE "reviews"."article_id" = 2 ORDER BY "reviews"."id"
DELETE from "reviews" WHERE "reviews"."id" = 13
DELETE from "reviews" WHERE "reviews"."id" = 15
DELETE from "reviews" WHERE "reviews"."id" = 16
DELETE from "reviews" WHERE "reviews"."id" = 18
...
```

This is called the N+1 queries problem. This could significantly slow down the application because it hits the database many times.

#### .delete_all
In fact, this could be done in one line of Ruby code and one SQL.

```ruby
@article.reviews.where(:comment, [nil, '']).delete_all
#or
@article.reviews.delete_all(:comment, [nil, ''])
```

The above code generates only one SQL.

```sql
DELETE FROM "reviews"
WHERE ("reviews"."name" = '' OR "reviews"."name" IS NULL)
AND "reviews"."article_id" = 2
```

#### .destroy_all

There’s another method .destroy_all which is different to .delete_all. In fact, .destroy_all also generates multiple queries. On each query, each object’s callbacks are executed while .delete_all ignore the callbacks. Therefore, if it is required to execute the callback after destroy, you can not use .delete_all. Use .destroy_all instead.

#### .update_all

Correspondingly, if we need to update multiple objects, we could use .update_all like the following:

```ruby
@article.reviews.where(:comment, [nil, '']).update_all(comment: "No comment")
```

This line generates the following SQL:

```SQL
UPDATE "reviews" SET "comment" = "No comment" WHERE
WHERE ("reviews"."name" = '' OR "reviews"."name" IS NULL)
AND "reviews"."article_id" = 2
```

Keep in mind that .update_all also ignores the callbacks and validations. If you want to make sure the callbacks and validations are called, use the following code:

```ruby
@article.reviews.where(:comment, [nil, '']).each do |r|
  r.update(comment: "No comment")
end
```

The method generates multiple SQL queries but all the callbacks and validations are called.

## 3. Solve the N+1 Queries problem for associations

Suppose there is a feature we need to display the titles of the current user’s articles. And for each article, we also want to show the rating of its first review. Then in the controller and the view, we may have the following code:

```
#controller
@articles = current_user.articles
#view
<% @articles.each do |article| %>
<p><%= article.title %>: <%= article.reviews.first.rating %></p>
<% end %>
```

Checking the server log, we may see something like this. Again, it is a N+1 queries problem.

```SQL
SELECT "articles".* FROM "articles" WHERE "articles"."user_id" = 12
SELECT "reviews".* FROM "reviews" WHERE "reviews"."article_id" = 13
SELECT "reviews".* FROM "reviews" WHERE "reviews"."article_id" = 14
SELECT "reviews".* FROM "reviews" WHERE "reviews"."article_id" = 15
SELECT "reviews".* FROM "reviews" WHERE "reviews"."article_id" = 16
SELECT "reviews".* FROM "reviews" WHERE "reviews"."article_id" = 17
```

The problem is due to when we load the articles from the current user, we did not tell rails to also load the reviews of each article. We could preload the associations of an ActiveRecord object by using three methods: .preload, .eager_load or .includes

#### .preload
When we use .preload, it preloads the associations of the object by using SELECT IN.

```ruby
#controller
@articles = current_user.articles.preload(:reviews)
```

.preload always generates two SQL queries.

```SQL
SELECT "articles".* FROM "articles" WHERE "articles"."user_id" = 12
SELECT "reviews".* FROM "reviews"  WHERE "reviews"."article_id" IN (13, 14, 15, 16, 17)
```

As a result, in the view when we called article.reviews.first.rating, it won’t hit the database anymore because the data are already loaded.

.preload very fast. But in some cases, it is not flexible. Think of the following code:

```ruby
Article.preload(:reviews).where("articles.title like '%Rails%'")
```

The line will throw an exception:

```
# =>
SQLite3::SQLException: no such column: articles.title:
SELECT "reviews".* FROM "reviews"  WHERE articles.title like '%Rails%'
```

As we can see, after .preload is called, the information of the parent object is lost.

#### .eager_load
Different to .preload, .eager_load uses LEFT OUTER JOIN to preload the associations

```ruby
Article.eager_load(:reviews)
```

```SQL
SELECT "articles"."id" AS t0_r0, "articles"."title" AS t0_r1,
"articles"."created_at" AS t0_r2, "articles"."updated_at" AS t0_r3,
"articles"."content" AS t0_r4, "articles"."user_id" AS t0_r5,
"reviews"."id" AS t1_r1, "reviews"."comment" AS t1_r2,
"reviews"."rating" AS t1_r3, "reviews"."article_id" AS t1_r4,
"reviews"."created_at" AS t1_r5, "reviews"."updated_at" AS t1_r6
FROM "articles" LEFT OUTER JOIN "reviews" ON "reviews"."article_id" = "articles"."id"
```

Therefore, we could continue to use .where(“articles.title like ‘%Rails%'”) without exceptions.

For common cases, SELECT IN is faster than LEFT OUTER JOIN so we tend to use .preload instead of .eager_load. In fact, the above code works if we change the order of .preload and .where.

```ruby
Article.where("articles.title like '%Rails%'").preload(:reviews)
```

#### .includes

.inlcudes is a combination of .preload and .eager_load. When it is possible, .includes uses the SELECT IN strategy. However, if we call Article.includes(:reviews).where(“articles.title like ‘%Rails%'”), it will use the LEFT OUTER JOIN strategy. As it is quite smart, Rails recommends using .includes for preloading associations.

## 4. Reuse cached data

Suppose that we need to display three tabs on a page. In one tab we want to show the reviews ordered by the submitted time. In another tab, we want to show the reviews with non empty comments and ordered by rating. In the last tab, we want to show all comments ordered by rating. How should we implement this? Normally, we may see the following code:

```ruby
#tab 1
@article.reviews.order(created_at: :desc)
#tab 2
@article.reviews.where.not(comment: [nil,'']).order(rating: :desc)
#tab 3
@article.reviews.where.order(rating: :desc)
```

The problem of the above code is that it generates 3 queries with results of the same dataset but not in different displays. A better solution is to use one query to get all the reviews of the article first. And then filter the objects and change the order by ruby methods. For example, we could have the following methods in the Article model:

```ruby
def reviews_order_by_rating
  self.reviews.sort { |r1, r2| r2.rating <=> r1.rating }
end

def commented_reviews_order_by_rating
  self.reviews.select { |r| r.comment.present? }
     .sort { |r1, r2| r2.rating <=> r1.rating }
end

def reviews_order_created_at
  self.reviews.sort { |r1, r2| r2.created_at <=> r1.created_at }
end
```

When we call the three methods one by one in the view, we only run one query in the first method call. After that, the second and third method calls will reuse the loaded reviews. Therefore, we reduce the database hits by reusing the cached reviews. Obviously, this works only when the number of reviews of an article is reasonable small and we don’t need to load them in chunks.

## 5. Use .pluck. only load required data
Now we need to implement a feature that generates a huge file which contains the titles of all the articles in the database. To achieve this, we may use the following code to return all the titles.

```ruby
Article.all.map(&:title)
```

```SQL
SELECT * from "articles"
```

The query not only retrieves all the titles but also get all the content from the database! If the title field has 50 characters in average, and the content field has 950 characters. This means 95% of memory is wasted! Instead of using .map naively, we could use pluck to save memory. It returns an array containing only the requested data.

```ruby
Article.pluck(:title)
# = ["title 1", "title 2", "title 3"]
```

```SQL
SELECT "articles.title" from "articles"
```

## 6. Use .find_in_batches or .find_in_each for batch processing

Let’s use the above example again. Let’s say we have ten million objects in the articles table. Even we use .pluck, it returns an array with ten million titles. This could lead to potential out of memory problem. For such cases, a wiser strategy is to retrieve the data from database in chunks. And each time we insert the subset of the data to the CSV file. .find_in_batches are the best to do the job.

```ruby
Article.find_each do |article|
  CSV.add_row([ article.title ])
end
#or
Article.find_in_batches do |articles|
  CSV.add_all_rows(articles.map(&:title))
end
```

By default, .find_each and .find_in_batches load 1000 records each time. This could be changed like .find_in_batches(batch_size: 2000).

With .pluck, we could only select required data. With .find_each and .find_in_batches, we could load data in chunks. Is there any way to combine the two methods? Is there any .pluck_in_batches? Unfortunately, the answer is no at least at the moment this article was posted. But we could achieve this by .select. .select returns the collection of the ActiveModel objects but only load the attributes you ask for. If you try to read an attribute that is not loaded, it will throw an MissingAttributeError.

```ruby
Article.select(:id, :title).find_each do |article|
  do_something_to(article.title)
end
```

## 7. Some times pure SQL works better

Suppose that we need to get the average rating of each article of the current user. We may use the following code:

```ruby
@articles = current_user.articles.preload(:reviews)
@articles.each do |article|
  reviews = article.reviews
  rating_map[article.id] = reviews.map(&:rating).sum/reviews.size
end
```

The above code first preloads all the reviews for each article and then calculates the average rating. Again, is it really necessary to load all the reviews to calculate the rating? If we are familiar with SQL, we probably could come up a query like the following:

```SQL
SELECT "articles".*, AVG(COALESCE("reviews"."rating",0))
AS "average_rating" FROM "articles"
LEFT OUTER JOIN "reviews" on "articles"."id" = "reviews"."article_id"
GROUP BY "articles"."id"
WHERE "articles"."user_id" = ?
``

Is there any way to achieve this query through ActiveRecord? It is absolutely yes. Here is the code:

```ruby
@articles = find_by_sql([ the_above_sql, current_user.id ])
# Then magically we could use article.average_rating to get the average rating.
# ActiveRecord automatically generates the attribute for us.
```

By using .find_by_sql, we could get the desired result trough only one query and no extra calculation.

## Summary: Don’t rely on ActiveRecord

Rails and ActiveRecord provide many magical and convenient methods. But we could not rely on them. Always check the SQL queries the code generates and ask yourself. Does it generate too many queries to the database? Does it only load necessary data? If not, figure out the correct queries and there must be some ways to implement that with ActiveRecord, even though executing pure SQL queries.
