---
layout:     post
title:      "Problem: Merge Intervals"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Sorting
    - Medium
---

## Question

Given a collection of intervals, merge all overlapping intervals.

For example,
Given `[1,3],[2,6],[8,10],[15,18]`,
return `[1,6],[8,10],[15,18]`.

## Solution
TODO

#### Code
```java
class Solution {
    public List<Interval> merge(List<Interval> intervals) {
        List<Interval> results = new ArrayList<>();
        if(intervals.size() == 0) return results;
        
        Collections.sort(intervals, (i1,i2) -> i1.start - i2.start);
        results.add(intervals.get(0));
        
        for(int i=1; i<intervals.size(); i++) {
            Interval last = results.get(results.size()-1);
            Interval cur = intervals.get(i);
            if(last.end >= cur.start) last.end = Math.max(last.end, cur.end);
            else results.add(cur);
        }
        
        return results;
    }
}
```

## Performance
TODO
