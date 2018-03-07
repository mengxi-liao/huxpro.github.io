---
layout:     post
title:      "Problem: Missing Numbers"
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

Given an array containing n distinct numbers taken from `0, 1, 2, ..., n`, find the one that is missing from the array.

**Example 1**

```
Input: [3,0,1]
Output: 2
```

**Example 2**

```
Input: [9,6,4,2,3,5,7,0,1]
Output: 8
```

Note:
Your algorithm should run in linear runtime complexity. Could you implement it using only constant extra space complexity?

## Solution 1

Here is a quick solution:

1. Setup a new array `res[n]`, initialize each element to `-1`.
2. Traverse the input array, for each element `nums[i]`, put it to `res[nums[i]]`. Ignore if `nums[i]` is greater than `n`.
3. Traverse the `res` array. For each element `res[i]`, if `res[i] == -1`, `i` is the missing number.

#### Optimization using swapping
Now as the question requires constant extra space, we could not setup the additional array `res`. That's often a hint that we need to construct the result by modifying the original array `nums`.

One way to do it is by using **swapping**. We could traverse the array. For each element, keep swapping `nums[i]` and `nums[nums[i]]` until `i == nums[i]`. if `nums[i] >= n`, mark it as `-1`. In the end, the missing number is `nums[i]` where `nums[i]==-1`.

Please check the following example to understand.

#### Example of using swapping:

```
Suppose the original array is `[0,4,1,2]`. Here n=4

i: 0, nums[0] = 0, so no swap. result is [0,4,1,2]
i: 1, nums[1] = 3, swap nums[1] and nums[3], result is [0,2,1,4]
i: 1, nums[1] = 2, swap nums[1] and nums[2], result is [0,1,2,4]
i: 1, nums[1] = 1, so no swap, result is [0,1,2,4]
i: 2, nums[2] = 2, so no swap, result is [0,1,2,4]
i: 3, nums[3] = 4, as nums[3] == n, set it to -1, result is [0,1,2,-1]

As nums[3] == -1, 3 is the missing number.
```

Here's an edge case: `[0,1]`. In this case, for each `nums[i]`, it equals to `nums[nums[i]]`. The first missing number should be `n` itself.

#### Code

Here is an implementation.

```java
class Solution {
    public int missingNumber(int[] nums) {
        for(int i=0; i<nums.length; i++) {
            while(nums[i] != -1 && nums[i] != i) {
                if(nums[i] == nums.length) {
                    nums[i] = -1;
                }
                else {
                    swap(nums, nums[i], i);
                }
            }
        }

        for(int i=0; i<nums.length; i++) {
            if(nums[i] == -1) return i;
        }

        return nums.length;
    }

    void swap(int[] nums, int i, int j) {
        int t = nums[i];
        nums[i] = nums[j];
        nums[j] = t;
    }
}
```

#### Performance

As on each swap, we will place at least one element to the right place. So there's at most n swaps in total. The time complexity is O(n). And as we are using the original array to store the result, only constant memory space is used.


## Solution 2

Another solution is based on a bit manipulation rule: `a^a^b = b`. 

So `0^nums[0]^...^(n-1)^nums[n-1]^n` is the missing number.

Here are a few examples:

```
For [0, 1]
0^0^1^1^2 = 2 where 2 is the missing number

For [0, 2]
0^0^2^1^2 = 1 where 1 is the missing number
```

#### Code

```java
class Solution {
    public int missingNumber(int[] nums) {
        int v = nums.length;
        for(int i=0; i<nums.length; i++) {
            v ^= nums[i]^i;
        }
        return v;
    }
}
```

#### Performance

As every element is visited once, the time complexity of the solution is O(1). Only constant extra space is used.
