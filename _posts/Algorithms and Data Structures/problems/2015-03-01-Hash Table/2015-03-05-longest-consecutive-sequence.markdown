---
layout:     post
title:      "Problem: Longest Consecutive Sequence"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Hard
---

## Question

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given `[100, 4, 200, 1, 3, 2]`,
The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.

Your algorithm should run in O(n) complexity.

## Solution
TODO

#### Code
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet();
        int max = 0;
        for(int num : nums) {
            set.add(num);
        }
        
        Iterator<Integer> itr = set.iterator();
        while(itr.hasNext()) {
            int val = itr.next();
            int upper = val;
            while(set.contains(upper)) {
                set.remove(upper);
                upper++;
            }
            int lower = val-1;
            while(set.contains(lower)) {
                set.remove(lower);
                lower--;
            }
            
            max = Math.max(max, upper-lower+1);
            
        }
        
        return max;
    }
}
```

## Performance
TODO
