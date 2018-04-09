---
layout:     post
title:      "Problem: Meeting Rooms"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Sorting
    - Easy
---

## Question

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...]` (si < ei), determine if a person could attend all meetings.

For example,
Given `[[0, 30],[5, 10],[15, 20]]`,
return `false`.
## Solution
TODO

#### Code
```java
class Solution {
    public boolean canAttendMeetings(Interval[] intervals) {
        if(intervals.length <= 1) return true;
        Arrays.sort(intervals, (i1, i2) -> i1.start - i2.start);
        for(int i=1; i<intervals.length; i++) {
            if(intervals[i].start < intervals[i-1].end) return false;
        }
        
        return true;
    }
}
```

## Performance
TODO
