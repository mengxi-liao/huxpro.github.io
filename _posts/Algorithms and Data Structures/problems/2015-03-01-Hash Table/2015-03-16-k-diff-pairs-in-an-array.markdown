---
layout:     post
title:      "Problem: K-diff Pairs in an Array"
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
    - Medium
    - Array
---

## Question

Given an array of integers and an integer k, you need to find the number of unique k-diff pairs in the array. Here a k-diff pair is defined as an integer pair (i, j), where i and j are both numbers in the array and their absolute difference is k.

**Example 1:**
```
Input: [3, 1, 4, 1, 5], k = 2
Output: 2
Explanation: There are two 2-diff pairs in the array, (1, 3) and (3, 5).
Although we have two 1s in the input, we should only return the number of unique pairs.
```

**Example 2:**
```
Input:[1, 2, 3, 4, 5], k = 1
Output: 4
Explanation: There are four 1-diff pairs in the array, (1, 2), (2, 3), (3, 4) and (4, 5).
```

**Example 3:**
```
Input: [1, 3, 1, 5, 4], k = 0
Output: 1
Explanation: There is one 0-diff pair in the array, (1, 1).
```

#### Code
```java
class Solution {
    public int findPairs(int[] nums, int k) {
        if(k<0) return 0;
        Map<Integer, Set<Integer>> map = new HashMap<>();
        Set<Integer> visited = new HashSet<>();

        for(int n:nums) {
            if(visited.contains(n-k)) {
                Set<Integer> set = map.getOrDefault(n-k, new HashSet<Integer>());
                set.add(n);
                map.put(n-k, set);
            }
            if(visited.contains(n+k)) {
                Set<Integer> set = map.getOrDefault(n, new HashSet<Integer>());
                set.add(n+k);
                map.put(n, set);
            }
            visited.add(n);
        }

        int count = 0;
        for(Map.Entry<Integer, Set<Integer>> entry : map.entrySet()) {
            count += entry.getValue().size();
        }

        return count;
    }
}
```

```java
class Solution {
    public int findPairs(int[] nums, int k) {
        if(k<0) return 0;
        Set<Integer> starts = new HashSet<>();
        Set<Integer> uniqs = new HashSet<>();

        int count = 0;
        for(int n:nums) {
            if(uniqs.contains(n+k)) starts.add(n);
            if(uniqs.contains(n-k)) starts.add(n-k);
            uniqs.add(n);
        }

        return starts.size();
    }
}
```

## Performance
O(n)
