---
layout:     post
title:      "Problem: Meeting Rooms II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Heap
    - Medium
---

## Question

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...] (si < ei)`, find the minimum number of conference rooms required.

For example,
Given `[[0, 30],[5, 10],[15, 20]]`,
return `2`.

## Solution
TODO

#### Code
```java
class Solution {
    public int minMeetingRooms(Interval[] intervals) {
        Arrays.sort(intervals, (i1, i2) -> i1.start - i2.start);
        PriorityQueue<Integer> pq = new PriorityQueue<Integer>();
        for(Interval i:intervals) {
            if(!pq.isEmpty() && pq.peek() <= i.start) {
                pq.poll();
            }
            pq.offer(i.end);
        }
        
        return pq.size();
    }
}
```

## Performance
TODO
