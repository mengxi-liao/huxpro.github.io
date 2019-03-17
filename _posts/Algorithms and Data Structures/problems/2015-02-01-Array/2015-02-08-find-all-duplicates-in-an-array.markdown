---
layout:     post
title:      "Problem: Find All Duplicates in an Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Given an array of integers, 1 ≤ a[i] ≤ n (n = size of array), some elements appear twice and others appear once.

Find all the elements that appear twice in this array.

Could you do it without extra space and in O(n) runtime?

**Example:**
```
Input:
[4,3,2,7,8,2,3,1]

Output:
[2,3]
```

## Solution

TODO

#### Code

```java
class Solution {
    public List<Integer> findDuplicates(int[] nums) {
        List<Integer> results = new ArrayList<Integer>();
        for(int i=0; i<nums.length; i++) {
            while(nums[i] != i+1 && nums[i] != -1) {
                int t=nums[i];
                if(nums[i] == nums[t-1]) {
                    results.add(nums[i]);
                    nums[i] = -1;
                }
                else {
                    nums[i] = nums[t-1];
                    nums[t-1] = t;
                }
            }
        }
        return results;
    }
}

```

#### Performance

O(n) time complexity and no extra space.
