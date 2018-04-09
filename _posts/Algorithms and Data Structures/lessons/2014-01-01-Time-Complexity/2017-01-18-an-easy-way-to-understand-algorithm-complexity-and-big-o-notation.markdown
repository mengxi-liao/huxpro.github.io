---
layout:     post
title:      "An Easy Way to Understand Algorithm Complexity and Big O Notation"
date:       2017-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Lesson
    - Algorithms and Data Structures
    - Algorithm Complexity
---

Big O notation is the most widely used method which describes algorithm complexity – the execution time required or the space used in memory or disk by an algorithm. Often in exams or interviews, you will be asked some questions about algorithm complexity in the following form. For an algorithm that uses a data structure of size n, what is the runtime complexity or space complexity of the algorithm? The answer to such questions often uses big O notations to describe the algorithm complexity, such as `O(1)`, `O(n)`, `O(n^2)` or `O(log(n))`.

# Big O for time complexity

Here we don’t want to discuss big O mathematically. When analyzing the time complexity of an algorithm, big O notation is used to describe the rough estimate of the number of “steps” to complete the algorithm. Let’s take the following example:

```java
void fun(int n) {

  // part1
  doSomething();

  // part2
  for(int j=0; j < n; j++)
    doSomething();

  // part3
  for(int i=0; i <  n; i++)
    for(int j=0; j < n; j++)
      doSomething();

  // part4
  return;
}
```

Here let’s assume that doSomething() takes C steps to complete. The whole `fun(n)` method has four parts. What is the time complexity of each part for different parameters `n`?

For part1, it does `doSomething()` so it takes constant `C` steps. Here `C` is independent of the parameter `n`. When the time complexity is independent of the parameter, we use `O(1)` to mark it.

For part2, it does `doSomething` `n` times. Each time it takes `C` steps. So in total, it takes `C x n` steps to complete part2. Then as described above, we use `O(1)` to complete the `C` steps. Then for `C x n`, the complexity becomes `n x O(1)`. Here, an important rule is that `a x O(n)` equals `O(a x n)`. In such case, `n x O(1) = O(n)`. So the time complexity of part2 is `O(n)`.

For part3, it has two loops. The inner loop is exactly like part2. The outer loop does part2 `n` times again, so the time complexity for part3 is `n x O(n)` which is `O(n^2)`.

For part4, it takes precisely 1 step to return. So the time complexity is `O(1)`.

Then what is the total time complexity of the whole `fun(n)`? It is easy; we just need to add up the time complexity of all the four parts:

```
O(1) + O(n) + O(n^2) + O(1)
```

Now let’s assume `n` becomes very very large. For part1 and part4, they still take constant `C+1` steps so the time running them could be ignored by part2 and part3, as now part2 and part3 take much longer time than part 1 and 4. Now if we compare part 2 and part 3. When `n` is 1, both part2 and part3 take `C` steps. When `n` is 3, part 2 takes `3C` steps while part 3 takes `9C` steps. When `n` is 1000, part 2 needs `1000C` steps but part3 takes `1000000C` steps! As `n` increases, the time complexity of part3 increases much faster than part 2. When `n` becomes extremely large, the time of part2 can be ignored by the time of part3.

So here is another rule, when adding up big O notations, the notation with slower increase speed could be ignored by the notation with faster increase speed. As we could see, `O(1)` does not increase at all so it could be ignored by `O(n)`. `O(n)` is slower than `O(n^2)` so it could be ignored by `O(n^2)`. Therefore, the complexity of the whole `fun()` is `O(n^2)`

# Rules summary of big O notations

From the above examples, we could summarize the following rules:

For multiplying two O notations, `O(A)` and `O(B)`, the result is `O(AB)`. For example:

```
O(1) x O(n) = O(n).

O(n) x O(n) = O(n^2).
```

For adding two O notations, `O(A)` and `O(B)`, the result is to choose the one with the faster increase speed. For example:
```
O(1) + O(n) = O(n).

O(n) + O(n^2) = O(n^2).

O(1) + O(n) + O(n^2) = O(n^2).
```

Here is the comparison of the increase speed of different O notations:

```
O(1) < O(log(n)) < O(n) < O(nlog(n)) < O(n^2)
```

# How to use big O notation to compare algorithm complexity and why

When comparing different algorithms, we often say the one with a “smaller” big O notation is more efficient. However, there are situations that algorithms with “larger” big O is faster. For example, there are two algorithms `f1(n)` and `f2(n)`. `f1(n)` takes 100 steps and `f2(n)` takes `n` steps so `f1(n)` is `O(1)` and `f2(n)` is `O(n)`. When `n` is less than 100, say `n` is 50, `f1(n)` takes 100 steps. `f2(n)` takes 50 steps so `f2(n)` is more efficient than `f1(n)`. However, when `n` goes up to 10000, `f2(n)` takes 10000 steps while `f1(n)` takes only 100 steps so `f1(n)` becomes way more efficient. As the nature of large-scale data in computer engineering, big O compares algorithms in the cases when the data is very large.

# Big O for space complexity

It is easier to understand using big O to estimate space complexity as it is more concrete. For example, in an algorithm, we need to create an array of size `n` to store the temporary results before getting the final result. If we assume that the size of the element in the array is a constant `C` which is independent of `n`, the space complexity of using the array is `Cn` which is `O(n) x O(C) = O(n) x O(1) = O(n)`.

When comparing different algorithms, we often compare how much “extra” space complexity is needed to solve the problem. For example, as an algorithm that needs an extra array of size `n` is not as good as the one which only needs two variables, `O(1)` space complexity is more efficient than `O(n)`.
