---
layout:     post
title:      "Problem: Serialize and Deserialize Binary Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Binary Tree
    - Binary Search Tree
    - Tree Set
    - Tree Map
    - Hard
---

## Question

Given an array of integers, find out whether there are two distinct indices i and j in the array such that the **absolute** difference between **nums[i]** and **nums[j]** is at most t and the **absolute** difference between i and j is at most k.

**Example 1:**
```
Input: nums = [1,2,3,1], k = 3, t = 0
Output: true
```
**Example 2:**
```
Input: nums = [1,0,1,1], k = 1, t = 2
Output: true
```
**Example 3:**
```
Input: nums = [1,5,9,1,5,9], k = 2, t = 3
Output: false
```

## Solution

This problem requires to maintain a window of size `k` of the previous values that can be queried for value ranges. The best data structure to do that is Binary Search Tree. As a result maintaining the tree of size k will result in time complexity `O(N lg K)`. In order to check if there exists any value of range `abs(nums[i] - nums[j])` to simple queries can be executed both of time complexity `O(lg K)`.

Here is the whole solution using `TreeSet`. `TreeSet` is implemented using a tree structure (Red-black tree in algorithm book, a red–black tree is a kind of self-balancing binary search tree). The elements in a set are sorted, but the add, remove, and contains methods has  time complexity of `O(log (n))`.

#### Code

Here is a sample solution.

```java
class Solution {
    public boolean containsNearbyAlmostDuplicate(int[] nums, int k, int t) {
        if(k==0) return false;
        TreeSet<Long> set = new TreeSet();
        for(int i=0; i<nums.length; i++) {
            Long ceiling = set.ceiling((long)nums[i]);
            Long floor = set.floor((long)nums[i]);
            if(floor != null && nums[i] - floor <= t) return true;
            if(ceiling != null && ceiling - nums[i] <= t) return true;
            
            if(set.size()==k) set.remove((long)nums[i-k]);
            
            set.add((long)nums[i]);
        }
        
        return false;
    }
}
```

## Performance

`O(N lg K)` time complexity as discussed.
