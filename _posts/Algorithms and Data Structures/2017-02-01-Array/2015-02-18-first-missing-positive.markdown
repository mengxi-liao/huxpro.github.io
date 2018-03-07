---
layout:     post
title:      "Problem: First Missing Positive"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
---

## Question

Given an unsorted integer array, find the first missing positive integer.

For example,
Given `[2,1,0]` return 3,
and `[3,4,-1,1]` return 2.

Your algorithm should run in `O(n)` time and uses constant space.

## Solution

The basic idea is to place each element in the array to its corresponding index so that `i=nums[i]-1` unless the element is not positive or greater than `n`. For example:

`[2,1,0]` could be converted to `[1,2,0]`. Note that `0` could be placed anywhere as it's not positive.
`[3,4,-1,1]` could be converted to `[1,-1,3,4]`. Note that `-1` could be placed anywhere.
`[3,5,-1,1]` could be converted to `[1,-1,3,-1]`. Note that `-1` could be placed anywhere. `5` could not be placed in the array, so mark it to `-1`.

Then, the first number where `nums[i]-1 != i` will be the first missing element. So for the first case, the first missing number is `3`. In the second case, the first missing number is `2`.

The problem now becomes how to convert the array efficiently without extra space. We could draw on the swapping idea from [The Missing Numbers](/2015/02/17/missing-numbers). Traverse the array. For each `nums[i]`, keep swapping `nums[i]` and `nums[nums[i]-1]` until `nums[i]-1 == i` or `nums[i]` is not positive or greater than `n`, . Here is an example:

```
For [2,1,0]

index 0, 2-1 != 0, swap 2 and 0, get [1,2,0]
index 0, 1-1 == 0, no swap, index = 1
index 1, 2-1 == 1, no swap, index = 2
index 2, 0 is not positive, no swap, index = 3 (end)

The missing number is 3
```

```
For [3,4,-1,1]

index 0, 3-1 != 0, swap 3 and 1, get [1,4,-1,3]
index 0, 1-1 == 0, no swap, index = 1
index 1, 4-1 != 1, swap 4 and 3, get [1,3,-1,4]
index 1, 3-1 != 1, swap 3 and -1, get [1,-1,3,4]
index 1, -1 is not positive, no swap, index = 2
index 2, 3-1 == 2, no swap, index = 3
index 3, 4-1 == 3, no swap, index = 4 (end)

The missing number is 2
```

#### Code

Here is an implementation.

```java
class Solution {
    public int firstMissingPositive(int[] nums) {
        for(int i=0; i<nums.length; i++) {
            while(nums[i]-1 != i && nums[i] > 0
                && nums[i] < nums.length
                && nums[i] != nums[nums[i]-1]) {

                swap(nums, i, nums[i]-1);
            }
        }

        for(int i=0; i<nums.length; i++) {
            if(nums[i]-1 != i) return i+1;
        }

        return nums.length+1;
    }


    private void swap(int[] nums, int i1, int i2) {
        int t = nums[i1];
        nums[i1] = nums[i2];
        nums[i2] = t;
    }
}
```

#### Performance

As everytime we swap `nums[i]` and `nums[nums[i]-1]`. We always place at least one number in the right place. So in total, we need at most `n` swapping. Overall the time complexity is `O(n).` And as it changes the numbers in the original array, the solution only needs `O(1)` extra space.