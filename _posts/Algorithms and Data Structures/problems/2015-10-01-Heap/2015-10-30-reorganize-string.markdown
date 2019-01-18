---
layout:     post
title:      "Problem: Reorganize String"
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

Given a string S, check if the letters can be rearranged so that two characters that are adjacent to each other are not the same.

If possible, output any possible result.  If not possible, return the empty string.

**Example 1:**
```
Input: S = "aab"
Output: "aba"
```

**Example 2:**
```
Input: S = "aaab"
Output: ""
```

**Note:**
- S will consist of lowercase letters and have length in range [1, 500].

## Solution
TODO

#### Code
```java
class Solution {
    public String reorganizeString(String S) {
        Map<Character, Integer> counters = new HashMap<>();
        for(int i=0; i<S.length(); i++) {
            char c = S.charAt(i);
            counters.put(c, counters.getOrDefault(c, 0)+1);
        }

        PriorityQueue<Character> pq = new PriorityQueue<>(
            (a, b) -> counters.get(b) - counters.get(a)
        );

        for(char c: counters.keySet()) {
            pq.add(c);
        }

        Character frozen = null;
        StringBuilder sb = new StringBuilder();
        while(!pq.isEmpty()) {
            char top = pq.poll();
            if(frozen != null) pq.add(frozen);
            if(counters.get(top) == 1) {
                counters.remove(top);
                frozen = null;
            }
            else {
                counters.put(top, counters.get(top)-1);
                frozen = top;
            }

            sb.append(top);
        }

        if(!counters.keySet().isEmpty()) return "";
        return sb.toString();
    }
}
```
