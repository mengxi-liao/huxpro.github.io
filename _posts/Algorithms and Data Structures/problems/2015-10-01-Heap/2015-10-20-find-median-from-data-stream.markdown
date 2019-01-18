---
layout:     post
title:      "Problem: Find Median from Data Stream"
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
    - Divide and Conquer
    - Hard
---

## Question

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

For example,
`[2,3,4]`, the median is 3

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

- void `addNum(int num)` - Add a integer number from the data stream to the data structure.
- double `findMedian()` - Return the median of all elements so far.

**Example:**

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3)
findMedian() -> 2
```

**Follow up:**

- If all integer numbers from the stream are between 0 and 100, how would you optimize it?
- If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?

## Solution
Use two heaps to keep track of the first half of the numbers and the second half of the numbers.

#### Code
```java
class MedianFinder {
    PriorityQueue<Integer> upper;
    PriorityQueue<Integer> lower;

    /** initialize your data structure here. */
    public MedianFinder() {
        upper = new PriorityQueue<Integer>();
        lower = new PriorityQueue<Integer>((a, b) -> b - a);
    }

    public void addNum(int num) {
        if(upper.isEmpty() || num > upper.peek()) upper.offer(num);
        else lower.offer(num);
        if(upper.size() > lower.size() + 1) lower.offer(upper.poll());
        else if(upper.size() < lower.size()) upper.offer(lower.poll());
    }

    public double findMedian() {
        int count = upper.size() + lower.size();
        if(count % 2 == 0) return (upper.peek() + lower.peek()) / 2.0;
        return upper.peek();
    }
}

/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */
```

## Performance
`O(1)` for `findMedian()`. `O(logn)` for `addNum()`.
