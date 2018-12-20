---
layout:     post
title:      "S.O.L.I.D in Ruby"
date:       2018-11-26 12:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Ruby on Rails
    - Ruby
    - OOP
    - Design Patterns
---

> "Ruby is the best object-oriented language.. if you use it in the right way"

For a long time working in the Ruby world, primarily working on Ruby on Rails projects, I found many projects do not follow proper Object Oriented programming practices. Ruby, as one of the most complete OOP language, provides tons of useful features to implement OOP. In this article, I will demonstrate how to write Ruby code comply with S.O.L.I.D. And some of the common anti-patterns those violate these principles in Ruby on Rails projects.

## What is S.O.L.I.D

One the most well-known sets of OO design principles are known by an acronym, SOLID. It stands for:

- Single responsibility principle (SRP)
- Open/closed principle (OCP)
- Liskov substitution principle (LSP)
- Interface segregation principle (ISP)
- Dependency inversion principle (DIP)

Let’s take a look at each of them individually, and how you can use them to increase your Ruby code’s quality.

## Single responsibility principle (SRP)

> "A class should have one, and only one, reason to change."

Let's interpret this a little bit. This also means when there is a requirement change, the class should only make the change for the responsibility it holds (so it only has one reason to change). 


#### Example

Let's look at the following example:

```ruby
class UserAuthenticator
  def authenticate(email, password)
    if matches?(email, password)
     do_some_authentication
    else
      raise NotAllowedError
    end
  end

  private
  def matches?(email, password)
    user = find_from_db(:user, email)
    user.encrypted_password == encrypt(password)
  end
end
```

The AuthenticatesUser class is responsible for authenticating the user as well as knowing if the email and password match the ones in the database. It has two responsibilities, and according to the principle it should only have one. Let’s extract one:

```ruby
class UserAuthenticator
  def authenticate(email, password)
    if PasswordMatcher.new(email, password).matches?
     do_some_authentication
    else
      raise NotAllowedError
    end
  end
end

class PasswordMatcher
  def initialize(email, password)
     @email = email
     @password = password
  end

  def matches?
    user = find_from_db(:user, @email)
    user.encrypted_password == encrypt(@password)
  end
end
```

#### Why

This makes change much harder!

- The more responsibilities a class has, the more likely we need to change the code in the class when there's requirement change.
- Code for one responsibility may couple to other responsibilities. Changing code for one feature may break other feature.

#### Anti-pattern: Fat Model

One of the most common anti-patterns in Rails is Fat model. In a lot of projects, I've seen developers implement business logic in the model class.

```ruby
class Account < ApplicationModel
  after_create :send_notification_email
  include ReportExportable # exports all accounts
  def signin ... end
  def register ... end
  def add_user(user) ... end
  def cancel ... end
end
```

The model then has a lot of responsibilities
- Holds data of the model record
- Handles database operations provided by ActiveRecord
- All different business logic (with methods, callbacks and concerns)

A fat model class could easily be expanded to hundreds of lines.

What we should do is to
- Use model classes as data holders and use service classes for bussiness logic
- Don't use controllers to handle business logic as it's only responsible for accepting request and returning response
- Concerns in models should only contain helpers for accessing its data.
- Callbacks should only be used for manipulating it's own data instead of doing any extra work.

```ruby
class Account < ApplicationModel
end

class SignupService
  def signup(account)
    ...
    SomeEmailSerive.send_notification_email
  end
end

def UserService
  def add_user(account, user) ... end
end

def ReportService
  def export(records) ... end
end
```

#### Anti-Pattern: Wrong way of extracting a method

We have a class `ContactPolicy` which extends `AccountResourcePolicy`

```ruby
class AccountResourcePolicy
  def show?
    user.account == resource.account
  end
end

class ContactPolicy < AccountResourcePolicy
  def show?
    return false if contact.organization != user.organization
    super
  end
end
```

And now we have another policy `DocumentPolicy` which also extends `AccountResourcePolicy`

```ruby
class ContactPolicy < AccountResourcePolicy
  def show?
    return false if contact.organization != user.organization
    super
  end
end
```

Ok now the developer may think maybe we should extract the duplicate code to a method for matching resource organization to the user's organization

```ruby
class AccountResourcePolicy
  def show?
    user.account == resource.account
  end

  protected
  def organization_matched?
    return false if contact.organization == user.organization
  end
end

class ContactPolicy < AccountResourcePolicy
  def show?
    return false unless organization_matched?
    super
  end
end

class DocumentPolicy < AccountResourcePolicy
  def show?
    return false unless organization_matched?
    super
  end
end
```

Extracting the common logic into a method does improve code reusability. However, the method should not be put into the base class as it is adding a responsibility which the base class should not be responsible for. A better approach is to create another class to handle the responsibility.

```ruby
class AccountResourcePolicy
  def show?
    user.account == resource.account
  end
end

class OrganizationMatcher
  def self.match?(user, resource)
    user.organization == resource.organization
  end
end

class ContactPolicy < AccountResourcePolicy
  def show?
    return false unless OrganizationMatcher.match?(user, resource)
    super
  end
end

class DocumentPolicy < AccountResourcePolicy
  def show?
    return false unless OrganizationMatcher.match?(user, resource)
    super
  end
end
```

## Open/closed principle (OCP)

> "You should be able to extend a classes behavior, without modifying it."

How can something be open and closed?! A class follows the OCP if it fulfills these two criteria:

- Open for extension

This ensures that the class behavior can be extended (by inheritance or composition). As requirements change, we should be able to make a new class behave in new and different ways by using the original class.

- Closed for modification

The source code of such a class is set in stone, no one is allowed to make changes to the code so that we don't need to change the code that uses this class.

#### Example

```ruby
class Report
  def body
     generate_reporty_stuff
  end

  def print
     body.to_json
  end
end
```

This code violates OCP, because if we want to change the format the report gets printed, you need to change the code of the class. Let’s change it then.

```ruby
class Report
  def body
     generate_reporty_stuff
  end

  def print(formatter: JSONFormatter.new)
     formatter.format body
  end
end
```

#### Why

This makes change much harder!

- Changing source code of exisitng classes may break clients those use this
- Adding new code becomes harder as there is no way to reuse existing code

#### How

- Make sure your code comply with SRP
- Anticipate where the change might happen. Make sure you class could adapt to the change (This is a technique for everything in software development...)

## Liskov Substitution Principle (LSP)

This one is complicated so let's talk about this in the end.

## Interface Segregation Principle

> "when a client depends upon a class that contains interfaces that the client does not use, but that other clients do use, then that client will be affected by the changes that those other clients force upon the class"

This one is simpler to demonstrate, if you have a class that has two clients (objects using it):

```ruby
class Car
  def open
  end

  def start_engine
  end

   def change_engine
   end
end

class Driver
  def drive
    @car.open
    @car.start_engine
  end
end

class Mechanic
  def do_stuff
    @car.change_engine
  end
end
```

As you can see, our Car class has an interface that’s used partially by both the Driver and the Mechanic. We can improve our interface like so:

```ruby
class Car
  attr_reader :control, :internals
end

class CarControl
  def open
  end
  def start_engine
  end
end

class CarInternals
  def change_engine
  end
  def change_wheels
  end
end

class Driver
  def drive
    @car_control.open
    @car_control.start_engine
  end
end

class Mechanic
  def do_stuff
    @car_internals.change_engine
  end
end
```

By splitting the interface into two, we can comply to the ISP.

## Dependency Inversion (DI)

> "Abstractions should not depend upon details. Details should depend upon abstractions."

Let’s go back to the first example on the OCP and change it a bit:

```ruby
class Report
  def body
     generate_reporty_stuff
  end

  def print
    JSONFormatter.new.format(body)
  end
end
```

Let's look at this example in deep. The `print` method clearly depends on the concrete class `JSONFormatter`. And the format it prints the report becomes dependent on how `JSONFormatter` prints the report.

To make this flexible, we allow the `print` method to accept a formatter. The `Report` class does not control the format anymore, but only provides the data of the report. And it does not need to know what type of formatter will be passed in to format the data. The only thing it needs to know is that the fomatter object accepts the `format` method. We call this programming to interface.


```ruby
class Report
  def body
     generate_reporty_stuff
  end

  def print(formatter)
    formatter.format body
  end
end
```

This simple example introduces an important technique in OOP - **Dependency Inversion**. Dependency inversion is relying on abstraction and programming to interface. In the above code, the `Report` class depends on a formatter object that accepts a `format` message, instead of a concrete formatter class. We could see the `formatter object that accepts a `format` message` as an interface that any concrete formatter class needs to implement. In Ruby, we don't have a concept of `interface` like java, but we could simulate the concept like this.

```ruby
class FormatterInterface
  def format
    raise NotImplementedError
  end
end

class JSONFormatter < FormatterInterface
  def format(data)
    # format data as json
  end
end
```

The `FormatterInterface` class is an abstraction of the `JSONFormatter`. And our report class is dependent on the abstraction instead of the concrete class, which makes changing the report format much more easily.

## Liskov Substitution Principle (LSP)

> "Derived classes must be substitutable for their base classes."

You may think this is easy, because we only need to make sure that the derived class is really a base class. But this is not sufficient. LSP is not only for class level but also for method level. Which means if you want to create a derived class, you need to make sure all the methods in the base class still works as expected in the derived class.

Here is an example:

```ruby
class Shape
end
class Rectangle < Shape
  def set_height ... end
  def set_width ... end
end
class Square < Rectangle
  def set_length ... end
end
```

Theoretically a square is indeed a rectangle, right? But when we implement this in code it may not be the case. A rectangle may accepts two messages `set_width` and `set_height` which allows the client to set the width and height of the rectangle with different lengths. However, for the Square class, it should only accept a `set_length` method. The `set_width` and `set_height` methods are not needed for the square. If we are forced to implement the two methods for the class, whenever we call `set_width` of a square, we have to to set its 'height' to make sure its width and height has the same length. In this case, we can clearly see that a Square class should not be extending the Rectangle class, because the behavior of the inherited methods differs.

#### Why

This breaks things!

- As the object of your new class may be used as an object of the existing classes and behave in an unexpected way.

[//]: # When we are working on the Office365 adapter, It's based on the Adapter class but it's requirement does not fully follow some of the existing logic in the adapter class. And this caused many bugs and we have to let QA find them and fix them one by one by overriding some of the methods.

#### How

- Follow SCP, OCP and ISP for your base class so your class is small, easier to understand and open for extension
- Don't make assumption on the methods in the base class if you think the behaviour might change
- Try to use Composition over Inheritance when we want to improve code reusability.

[//]: # Review policy classes (PromoPolicy and AccountResourcePolicy)

#### Anti-Pattern: Wrong way of override a method

When we override a method, remember to check if the method breaks LSP. After the method is override, it should still have the expected behaviour of the method in the base class.

Let's review `Adapter#pull_and_handle_orphaned_records`, `SyncGodBase#pull_and_handle_orphaned_records!`.

```ruby
class Adapter
  def full_sync!
    ...
    ...
    pull_and_handle_orphaned_records(...)
  end

  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    ...
    orphan_retry_ids.each do |adapters_resource_id|
      self.delegate_pull!(type_singular, AdaptersResource.find(adapters_resource_id))
    end
    # ...
    mark_missing_records_as_orphaned!(...)
  end
end

class SyncGodBase < Adapter
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    # ...
    orphan_adapters_resources.find_each do |adapters_resource|
      adapters_resource.resource.try(:force_destroy) if adapters_resource.resource_id
      adapters_resource.destroy
    end
  end
end
```

## Some Real World examples

#### Adapter#pull_and_handle_orphaned_records

Before we move to the actual refactoring, let's think about why the adapter class is bad (We know it is bad) and why we end up with the classes.

The class was created many years ago, and when it is implemented, it probably looks like this:

```ruby
class Adapter
  def pull_organizations! ... end
  def pull_locations! ... end
  def pull_contacts! ... end
  def pull_configurations! ... end

  def full_sync!
    ...
    pull_organizations!
    pull_locations!
    pull_configurations!
    ...

    # some logic to handle orphaned records
  end
end
```

First, this obviously is a fat model that violates the SRP. We would like to turn this into a service at the very beginnning.

```ruby
class AdapterService
  def pull_organizations! ... end
  def pull...

  def full_sync!
    ...
    pull_organizations!
    ...

    # some logic to handle orphaned records
  end
end
```

Now we need some other integrations implemented, but they are provided by `Sync God` so we want to abstract a `SyncGodBaseService` will be a good idea. And the developer thought `SyncGodBaseService` should extend the `AdapterService` class.

```ruby
class SyncGodBaseService < AdapterService
  ...
end
```

So `SyncGod#full_sync!` follows most of the logic in the `full_sync!` method. However, it handles orphaned records a bit differently. So the developer decided to extract the logic for handling orphaned records in `AdapterService` to a new `pull_and_handle_orphaned_records` method. and then let `SyncGodBaseService` overrides the method. Now the method in the `Adapter` class marks adapter resources as orphan but the overriden method in `SyncGodBase` deletes the adapter resource.

```ruby
class AdapterService
  def full_sync!
    ...
    ...
    pull_and_handle_orphaned_records(...)
  end

  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    ...
    orphan_retry_ids.each do |adapters_resource_id|
      self.delegate_pull!(type_singular, AdaptersResource.find(adapters_resource_id))
    end
    # ...
    mark_missing_records_as_orphaned!(...)
  end
end

class SyncGodBaseService < AdapterService
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    # ...
    orphan_adapters_resources.find_each do |adapters_resource|
      adapters_resource.resource.try(:force_destroy) if adapters_resource.resource_id
      adapters_resource.destroy
    end
  end
end
```

What is the issue of this approach. As we could see the behaviour of the two methods are almost totally different. This indicates the two classes violate the Liskov substitution principle (LSP). Either the `SyncGodBase` is not an `Adapter` or the `Adapter` class has implemented too much for a base class.

The problem here is in the `AdapterService`, it makes the assumption that orphaned records are handled by marking all the records as orphaned, while some other `AdapterService` may handle this in a different ways. Be caution when making assumption in the base class. Because when making assumption, you are creating a contract and the sub class may break the contract after overriding the methods.

To resolve this, we should not make the assumption in a base class. Here is a better approach:

```ruby
class AdapterService
  def full_sync!
    ...
    ...
    pull_and_handle_orphaned_records(...)
  end

  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    raise NotImplementedError
  end
end

class AdapterServiceA < AdapterService
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    ...
    orphan_retry_ids.each do |adapters_resource_id|
      self.delegate_pull!(type_singular, AdaptersResource.find(adapters_resource_id))
    end
    # ...
    mark_missing_records_as_orphaned!(...)
  end
end

class SyncGodBaseService < AdapterService
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    # ...
    orphan_adapters_resources.find_each do |adapters_resource|
      adapters_resource.resource.try(:force_destroy) if adapters_resource.resource_id
      adapters_resource.destroy
    end
  end
end
```

Here we have used a design pattern called *Template Pattern*. Now these classes do not violate the Liskov substitution principle (LSP).

But here is another issue, if we want to implement a `AdapterServiceB`, we will need to implement the `#pull_and_handle_orphaned_records` exactly the same to the one in `AdapterServiceA`. How could we reduce the duplicate codes accross differen classes.

The root problem is that `AdapterServiceA` and `AdapterServiceB` violate the Single Responsibility Principle (SRP). The adapter classes should not know how to find orphaned records and how to mark them as orphaned. What we could do is to extract the logics to some `OrphanedRecordHandler` classes.

```ruby
class OrphanedRecordHandler
  def handle!(type, synced_adapters_resource_ids)
    raise NotImplementedError
  end
end

class RetryAndMarkAsOrphanedRecordHandler < OrphanedRecordHandler
  def handle!(type, synced_adapters_resource_ids)
    # retry and mark orphaned records as orphaned
  end
end

class DeleteOrphanedRecordHandler < OrphanedRecordHandler
  def handle!(type, synced_adapters_resource_ids)
    # delete orphaned records
  end
end

class AdapterServiceA < AdapterService
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    RetryAndMarkAsOrphanedRecordHandler.new.handle!(type, synced_adapters_resource_ids)
  end
end

class AdapterServiceB < AdapterService
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    RetryAndMarkAsOrphanedRecordHandler.new.handle!(type, synced_adapters_resource_ids)
  end
end

class SyncGodBaseAdapterService < AdapterService
  def pull_and_handle_orphaned_records!(type, synced_adapters_resource_ids)
    DeleteOrphanedRecordHandler.new.handle!(type, synced_adapters_resource_ids)
  end
end
```

This example introduces another important design pattern which is the *Strategy Pattern*. Strategy Pattern uses abstraction to encaupsulate different algorithms.
