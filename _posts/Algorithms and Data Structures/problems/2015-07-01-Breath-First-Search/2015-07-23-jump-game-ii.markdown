---
layout:     post
title:      "Problem: Jump Game II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Breadth First Search
    - Medium
---

## Question

Given an array of non-negative integers, you are initially positioned at the first index of the array.

Each element in the array represents your maximum jump length at that position.

Your goal is to reach the last index in the minimum number of jumps.

Example:
```
Input: [2,3,1,1,4]
Output: 2
Explanation: The minimum number of jumps to reach the last index is 2.
    Jump 1 step from index 0 to 1, then 3 steps to the last index.
```

## Solution

Use BFS

#### Code
```java
class Solution {
    public int jump(int[] nums) {
        if(nums.length == 1) return 0;
        int start = 0;
        int end = 0;
        int level = 0;
        while(start <= end) {
            level++;
            int curEnd = end;
            for(int i=start; i<=curEnd && i<nums.length; i++) {
                if(i+nums[i] >= end) {
                    end = i+nums[i];
                    if(end >= nums.length-1 )  return level;
                }
            }
            start = curEnd+1;
        }
        return -1;
    }
}
```

## Performance

TODO
