---
layout:     post
title:      "Problem: Contains Duplicate II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
---

## Question

Given an array of integers and an integer k, find out whether there are two distinct indices i and j in the array such that `nums[i] = nums[j]` and the **absolute** difference between i and j is at most k.

## Solution
TODO

#### Code
```java
class Solution {
    public boolean containsNearbyDuplicate(int[] nums, int k) {
        Set<Integer> set = new HashSet<>();
        for(int i=0; i<nums.length; i++) {
            if(set.contains(nums[i])) return true;
            set.add(nums[i]);
            if(set.size() > k) set.remove(nums[i-k]);
        }
        
        return false;
    }
}
```

## Performance
TODO