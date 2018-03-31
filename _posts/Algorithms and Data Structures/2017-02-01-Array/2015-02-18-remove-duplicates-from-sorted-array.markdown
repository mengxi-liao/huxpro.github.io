---
layout:     post
title:      "Problem: Remove Duplicates from Sorted Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Two Pointers
---

## Question

Given a sorted array, remove the duplicates in-place such that each element appears only once and return the new length.

Do not allocate extra space for another array, you must do this by modifying the input array in-place with O(1) extra memory.

**Example:**

```
Given nums = [1,1,2],

Your function should return length = 2, with the first two elements of nums being 1 and 2 respectively.
It doesn't matter what you leave beyond the new length.
```

## Solution 1

As the array is sorted, we know that duplicate numbers are consecutive in the array. By Traversing the array, we could check if the element is a duplicate by checking the previous element. When a new element is found, add that to the result. If the element is a duplicate, skipped it safely.

#### Code

Here is an implementation.

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int l = 0;
        for(int i=0; i<nums.length; i++)
            if(i==0 || nums[i] != nums[i-1]) 
                // here: i must be the first number in a  
                // sequence of duplicate elements
                nums[l++] = nums[i];
        return l;
    }
}
```


## Solution 2

Another solution splits the problem into two subproblems.
1. Let's consider the sorted array as a sequence of groups of duplicate elements. We need to add the first element of each group to the result. So we need an outer loop and every time it enters the loop, make sure the index is pointing at the first element of a group.
2. In each iteration of the outer loop, move the index to the first element to the next group. This could be done by an inner loop.

#### Code

```java
class Solution {
    public int removeDuplicates(int[] nums) {
        int fast=0;
        int slow = 0;
        while(fast<nums.length) {
            # when we enters the loop, fast is always pointing to the 
            # to the first element of the current loop.
            nums[slow++] = nums[fast++];

            # make sure fast points to the first element of the next group
            while(fast<nums.length && nums[fast] == nums[fast-1]) fast++;
        }

        return slow;
    }
}
```

## Performance

In both solutions, each element in the array is visited once so the time complexity is `O(n)`. We used the original array to store the result so `O(1)` extra space is used.
