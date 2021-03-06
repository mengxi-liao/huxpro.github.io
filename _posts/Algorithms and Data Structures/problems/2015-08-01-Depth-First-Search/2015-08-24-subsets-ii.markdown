---
layout:     post
title:      "Problem: Subsets II"
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

Given a set of distinct integers, nums, return all possible subsets (the power set).

Note: The solution set must not contain duplicate subsets.

For example,
If nums = `[1,2,3]`, a solution is:

```
[
  [3],
  [1],
  [2],
  [1,2,3],
  [1,3],
  [2,3],
  [1,2],
  []
]
```

**Follow up**

What if the set has duplicate integers?

For example,
If nums = `[1,2,2]`, a solution is:

```
[
  [2],
  [1],
  [1,2,2],
  [2,2],
  [1,2],
  []
]
```

## Solution
TODO 

#### Code
```java
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums); // only for duplicate
        List<Integer> subset = new ArrayList();
        List<List<Integer>> results = new ArrayList();
        collectSubsets(subset, results, nums, 0); 
        return results;
    }

    public void collectSubsets(List<Integer> subset, List<List<Integer>> results, int[] nums, int idx) {
        results.add(new ArrayList(subset));
        for(int i=idx; i<nums.length; i++) {
            if(i>idx && nums[i] == nums[i-1]) continue; // to skip duplicate
            subset.add(nums[i]);
            collectSubsets(subset, results, nums, i+1);
            subset.remove(subset.size()-1);
        }
    }
}
```

## Performance
TODO
