---
layout:     post
title:      "Problem: Single Number"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Medium
---

## Question

Given an array of integers, every element appears twice except for one. Find that single one.

**Note:**
Your algorithm should have a linear runtime complexity. Could you implement it without using extra memory?

## Solution 1
TODO

#### Code
```java
class Solution {
    public int singleNumber(int[] nums) {
        Set<Integer> set = new HashSet();
        for(int i=0; i<nums.length; i++) {
            if(set.contains(nums[i])) {
                set.remove(nums[i]);
            }
            else {
                set.add(nums[i]);
            }
        }
        
        return set.iterator().next();
    }
}
```

## Solution 2
TODO

#### Code
```java
class Solution {
    public int singleNumber(int[] nums) {
        int xor = nums[0];
        for(int i=1; i<nums.length; i++) {
            xor = xor ^ nums[i];
        }
        
        return xor;
    }
}
```

## Performance
TODO
