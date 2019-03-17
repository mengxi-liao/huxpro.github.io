---
layout:     post
title:      "Problem: Combination Sum II"
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

Given a set of candidate numbers (candidates) (without duplicates) and a target number (target), find all unique combinations in candidates where the candidate numbers sums to target.

The same repeated number may be chosen from candidates unlimited number of times. Each number in candidates may only be used once in the combination.

**Note:**

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.

**Example 1:**
```
Input: candidates = [10,1,2,7,6,1,5], target = 8,
A solution set is:
[
  [1, 7],
  [1, 2, 5],
  [2, 6],
  [1, 1, 6]
]
```

**Example 2:**
```
Input: candidates = [2,5,2,1,2], target = 5,
A solution set is:
[
  [1,2,2],
  [5]
]
```

## Solution

DFS

#### Code
```java
class Solution {
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        List<Integer> result = new ArrayList<>();
        List<List<Integer>> results = new ArrayList<>();
        dfs(candidates, 0, target, result, results);
        return results;
    }

    public void dfs(int[] candidates, int start, int target, List<Integer> result, List<List<Integer>> results) {
        if(target == 0) {
            results.add(new ArrayList<>(result));
            return;
        }
        if(target < 0) return;
        for(int i=start; i<candidates.length; i++) {
            if(i>start && candidates[i] == candidates[i-1]) continue;
            if(result.size()>0 && result.get(result.size()-1) > candidates[i]) continue;
            result.add(candidates[i]);
            dfs(candidates, i+1, target-candidates[i], result, results);
            result.remove(result.size()-1);
        }
    }
}
```
