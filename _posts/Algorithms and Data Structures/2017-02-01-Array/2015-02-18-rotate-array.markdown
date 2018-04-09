---
layout:     post
title:      "Problem: Rotate Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
---

## Question

Rotate an array of n elements to the right by k steps.

For example, with `n = 7` and `k = 3`, the array `[1,2,3,4,5,6,7]` is rotated to `[5,6,7,1,2,3,4]`.

## Solution

We could solve the problem by 3 `reverse` operations. For example, `nums = [1,2,3,4,5,6,7]` and `k = 3`. First we reverse the array as a whole, it becomes `[7,6,5,4,3,2,1]`. Then we reverse the first `k` elements, it becomes `[5,6,7,4,3,2,1]`. Last we reverse the last `n-k` elemets, it becomes `[5,6,7,1,2,3,4]`.

The reverse is done by using two pointers, one pointer at the head and the other point at the tail, after switch these two, these two pointers move one position towards the middle.

#### Code

Here is a sample solution.

```java
class Solution {
    public void rotate(int[] nums, int k) {
        k = k % nums.length;
        //reverse the whole array first
        reverse(nums, 0, nums.length - 1);
        reverse(nums, 0, k-1);
        reverse(nums, k, nums.length - 1);
    }

    public void reverse(int[] nums, int start, int end) {
        while(start <= end) {
            int temp = nums[start];
            nums[start] = nums[end];
            nums[end] = temp;
            start ++;
            end --;
        }
    }
}
```

## Performance

The reverse function is an O(n) operation. The time complexity of the three reverse calls is

```
O(k) + o(n-k) + O(n) => O(n)
```

Only constant extra space is used in the algorithm.
