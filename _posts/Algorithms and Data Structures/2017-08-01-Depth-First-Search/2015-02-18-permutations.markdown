---
layout:     post
title:      "Problem: Permutations"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
---

## Question

Given a collection of distinct numbers, return all possible permutations.

For example,
`[1,2,3]` have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

**Follow up:**
What if the collection has duplicate numbers?

## Solution
TODO

#### Code
```java
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> results = new ArrayList();
        collect(nums, 0, results);
        return results;
    }
    
    private void collect(int[] nums, int idx, List<List<Integer>> results) {
        if(idx == nums.length) {
            List<Integer> list = new ArrayList();
            for(int n:nums) list.add(n);
            results.add(list);
            return;
        }
        
        // start form idx, not idx+1

        /* if permuteUnique */
        Set<Integer> visited = new HashSet<>();
        /* if permuteUnique */

        for(int i=idx; i<nums.length; i++) {

            /* if permuteUnique */
            if(visited.contains(nums[i])) continue;
            visited.add(nums[i]);
            /* if permuteUnique */

            swap(nums, idx, i);
            collect(nums, idx+1, results);
            swap(nums, idx, i);
        }
    }
    
    private void swap(int[] nums, int i1, int i2) {
        int t = nums[i1];
        nums[i1] = nums[i2];
        nums[i2] = t;
    }
}
```

## Performance
TODO