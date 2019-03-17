---
layout:     post
title:      "Problem: Matchsticks to Square"
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
    - Union Find
    - Hard
---

## Question

Remember the story of Little Match Girl? By now, you know exactly what matchsticks the little match girl has, please find out a way you can make one square by using up all those matchsticks. You should not break any stick, but you can link them up, and each matchstick must be used exactly one time.

Your input will be several matchsticks the girl has, represented with their stick length. Your output will either be true or false, to represent whether you could make one square using all the matchsticks the little match girl has.

**Example 1:**
```
Input: [1,1,2,2,2]
Output: true
```

Explanation: You can form a square with length 2, one side of the square came two sticks with length 1.

**Example 2:**
```
Input: [3,3,3,3,4]
Output: false
```

Explanation: You cannot find a way to form a square with all the matchsticks.

## Solution

DFS

#### Code
```java
class Solution {
    public boolean makesquare(int[] nums) {
        if(nums.length < 4) return false;
        int sum = 0;
        for(int n:nums) sum += n;
        if(sum % 4 != 0) return false;
        Arrays.sort(nums);
        int[] sums = new int[4];

        return dfs(nums, nums.length-1, sums, sum / 4);
    }

    private boolean dfs(int[] nums, int idx, int[] sums, int len) {
        if(idx == -1) return true;
        for(int i=0; i<sums.length; i++) {
            if(sums[i] + nums[idx] <= len) {
                sums[i] += nums[idx];
                if(dfs(nums, idx-1, sums, len)) return true;
                sums[i] -= nums[idx];
            }
        }

        return false;
    }
}

```

#### Performance
O(4^N)
