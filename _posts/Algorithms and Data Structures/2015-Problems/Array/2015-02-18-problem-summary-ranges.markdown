---
layout:     post
title:      "Problem: Summary Ranges"
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

Given a sorted integer array without duplicates, return the summary of its ranges.

```
Example 1:
Input: [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
```

```
Example 2:
Input: [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
```

## Solution

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList();
        int i=0;
        while(i<nums.length) {
            // when entering this loop
            // i is always at the starting of a range
            int s=i;

            // find the start of the next range
            while(i<nums.length && nums[i]-nums[s] == i-s) i++;

            if(s==i-1) res.add(""+nums[s]);
            else res.add(nums[s] + "->" + nums[i-1]);
        }

        return res;
    }
}
```
