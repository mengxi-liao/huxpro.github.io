---
layout:     post
title:      "Problem: Combination Sum"
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

The same repeated number may be chosen from candidates unlimited number of times.

**Note:**

All numbers (including target) will be positive integers.
The solution set must not contain duplicate combinations.

**Example 1:**
```
Input: candidates = [2,3,6,7], target = 7,
A solution set is:
[
  [7],
  [2,2,3]
]
```

**Example 2:**
```
Input: candidates = [2,3,5], target = 8,
A solution set is:
[
  [2,2,2,2],
  [2,3,3],
  [3,5]
]
```

## Solution

DFS

#### Code
```java
class Solution {
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        Arrays.sort(candidates);

        List<List<Integer>> results = new ArrayList<>();
        List<Integer> res = new ArrayList<>();

        dfs(candidates, 0, target, results, res);

        return results;
    }

    public void dfs(int[] candidates, int start, int target, List<List<Integer>> results, List<Integer> res) {
        if(target < 0) return;
        if(target == 0) {
            results.add(new ArrayList<Integer>(res));
            return;
        }

        for(int i=start; i<candidates.length; i++) {
            res.add(candidates[i]);
            dfs(candidates, i, target-candidates[i], results, res);
            res.remove(res.size()-1);
        }
    }
}
```
