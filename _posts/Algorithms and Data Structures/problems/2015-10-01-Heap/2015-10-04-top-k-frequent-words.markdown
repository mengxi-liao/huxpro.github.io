---
layout:     post
title:      "Problem: Top K Frequent Words"
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

Given a non-empty list of words, return the k most frequent elements.

Your answer should be sorted by frequency from highest to lowest. If two words have the same frequency, then the word with the lower alphabetical order comes first.

**Example 1:**
```
Input: ["i", "love", "leetcode", "i", "love", "coding"], k = 2
Output: ["i", "love"]
Explanation: "i" and "love" are the two most frequent words.
Note that "i" comes before "love" due to a lower alphabetical order.
```

**Example 2:**
```
Input: ["the", "day", "is", "sunny", "the", "the", "the", "sunny", "is", "is"], k = 4
Output: ["the", "is", "sunny", "day"]
Explanation: "the", "is", "sunny" and "day" are the four most frequent words,
    with the number of occurrence being 4, 3, 2 and 1 respectively.
```

**Note:**
- You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
- Input words contain only lowercase letters.

**Follow up:**
Try to solve it in O(n log k) time and O(n) extra space.

## Solution
TODO

#### Code
```java
class Solution {
    public List<String> topKFrequent(String[] words, int k) {
        Map<String, Integer> map = new HashMap<>();
        for(String w:words) {
            map.put(w, map.getOrDefault(w,0)+1);
        }

        PriorityQueue<String> pq = new PriorityQueue<String>(
            (a,b) -> map.get(a).equals(map.get(b)) ? b.compareTo(a) : map.get(a) - map.get(b)
        );

        for(String w:map.keySet()) {
            pq.offer(w);
            if(pq.size()>k) pq.poll();
        }

        List<String> results = new ArrayList<>();
        while(!pq.isEmpty()) results.add(0, pq.poll());

        return results;
    }
}
```

## Performance
TODO
