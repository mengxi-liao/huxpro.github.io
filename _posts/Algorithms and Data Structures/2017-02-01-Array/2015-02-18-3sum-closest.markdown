---
layout:     post
title:      "Problem: 3Sum Closest"
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

Given an array S of n integers, find three integers in S such that the sum is closest to a given number, target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

```
For example, given array S = {-1 2 1 -4}, and target = 1.
The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).
```

## Solution
TODO

#### Code
```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int closest = nums[0] + nums[1] + nums[2];
        for(int i=0; i<nums.length-2; i++) {
            int l = i+1;
            int r = nums.length-1;
            while(l<r) {
                int sums = nums[i] + nums[l] + nums[r];
                if(Math.abs(target - sums) < Math.abs(target - closest))
                    closest = sums;
                if(closest == target) return closest;
                
                if(target > sums) {
                    l++;
                }
                else {
                    r--;
                }
            }
        }
        
        return closest;
    }
}
```

#### Performance
TODO