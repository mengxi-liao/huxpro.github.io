---
layout:     post
title:      "Problem: Combination Sum III"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Medium
---

## Question

Find all possible combinations of k numbers that add up to a number n, given that only numbers from 1 to 9 can be used and each combination should be a unique set of numbers.

**Note:**

- All numbers will be positive integers.
- The solution set must not contain duplicate combinations.

**Example 1:**
```
Input: k = 3, n = 7
Output: [[1,2,4]]
```

**Example 2:**
```
Input: k = 3, n = 9
Output: [[1,2,6], [1,3,5], [2,3,4]]
```

## Solution

DFS

#### Code
```java
class Solution {
    public List<List<Integer>> combinationSum3(int k, int n) {
        List<List<Integer>> results = new ArrayList<>();
        List<Integer> result = new ArrayList<>();
        dfs(1, k, n, result, results);
        return results;
    }

    private void dfs(int start, int k, int n, List<Integer> result, List<List<Integer>> results) {
        if(k==0 && n==0) {
            results.add(new ArrayList<>(result));
            return;
        }
        if(k<0 || n<0) return;
        for(int i=start; i<=9; i++) {
            result.add(i);
            dfs(i+1, k-1, n-i, result, results);
            result.remove(result.size()-1);
        }
    }
}
```
