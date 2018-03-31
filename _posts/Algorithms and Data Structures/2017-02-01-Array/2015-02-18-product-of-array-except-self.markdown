---
layout:     post
title:      "Problem: Product of Array Except Self"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Given an array of n integers where `n > 1`, `nums`, return an array output such that `output[i]` is equal to the product of all the elements of nums except `nums[i]`.

Solve it without division and in `O(n)`.

For example, given `[1,2,3,4]`, return `[24,12,8,6]`.

**Follow up:**

Could you solve it with constant space complexity? (Note: The output array does not count as extra space for space complexity analysis.)

## Solution

#### The wrong approach

By glancing the problem, we may think of a solution by first calculating the product of all elements in the array. Then, to get corresponding product-except-self result, `o[i]`, of an element, `nums[i]`, divide the product by `nums[i]`.

This solution won't work if there's `0` in the array.

#### Brutal force
Another idea is to, for each `nums[i]`, calculate the product of the other elements. This brutal force solution needs to traverse all the other elements for each element, so its time complexity is `O(n^2)`. And `O(n)` extra space as a new array is needed to store the result.

#### Remove duplicate operations
From the brutal force algorithm, you may notice there are duplicate operations.

Example:
To get `o[i]`, we caculate the product of
```
prod_before[i] = nums[0] * nums[1] * .. * nums[i-1]  
prod_after[i] = nums[i+1] * nums[i+2] * .. * nums[n-1]
```


To get `o[i+1]`, we caculate the product of 
```
prod_before[i+1] = nums[0] * nums[1] * .. * nums[i] and 
prod_after[i+1] = nums[i+2] * nums[i+3] * .. * nums[n-1]
```

So 

```
prod_before[i+1] = prod_before[i] * nums[i]
prod_after[i] = nums[i+1] * prod_after[i+1]
```

With that, we could get a more efficient solution.
1. Traverse `nums` from its start, caculate an array of `prod_before` such that `prod_before[0]` = 1. `prod_before[i]` is the product of all the elements before `nums[i]`. `prod_before[i]` can be calculated by `prod_before[i-1]*nums[i]`.
2. Traverse `nums` from its end, calculate an array of `prod_after` such that `prod_after[n-1]` = 1. `prod_after[i]` is the product of all the elements after `nums[i]`. `prod_after[i]` can be calculated by `nums[i+1] * prod_after[i+1]`.
3. Traverse `nums` again, for each `nums[i]`, its product-except-self `o[i]` is `prod_before[i] * prod_after[i]`.

This solution requires O(n) time complexity and O(n) extra space.


#### Space Optimization

You may notice that we could use the output array `o` itself to store `prod_before`. Then, in the second step, we just need a `prod_after` variable to keep track of `prod_after[i]` as `prod_after` for the current `nums[i]` can be calculated by `prod_after * nums[i]`.
And `o[i] = prod_after * prod_before[i]` which is `prod_after * prod_before[i]`.

## Code

Here is a sample solution.

```java
class Solution {
    public int[] productExceptSelf(int[] nums) {
        int[] o = new int[nums.length];
        int prod = 1;
        for(int i=0; i<=nums.length-1; i++) {
            // o[i] is the prod of all the elements before itself.
            o[i] = prod;
            prod *= nums[i];
        }
        
        prod = 1;
        for(int i=nums.length-1; i>=0; i--) {
            // o[i] is the o[i] * prod of all the elements after itself.
            o[i] = o[i]*prod;
            prod *= nums[i];
        }
        
        return o;
    }
}
```

## Performance

The solution uses two loops to traverse each `num[i]` once, so the overall time complexity is `O(n)`. Besides the original array, `nums` and output `o`, only constant extra space is used.
