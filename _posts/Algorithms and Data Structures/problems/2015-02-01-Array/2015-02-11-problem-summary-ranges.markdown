---
layout:     post
title:      "Problem: Summary Ranges"
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
    - Easy
---

## Question

Given a sorted integer array without duplicates, return the summary of its ranges.

```
Example 1:
Input: [0,1,2,4,5,7]
Output: ["0->2","4->5","7"]
```

```
Example 2:
Input: [0,2,3,4,6,8,9]
Output: ["0","2->4","6","8->9"]
```

## Solution

This problem has two subproblems. 
- We need to list all the ranges from the array. 
- For each range, we need to find its start element and its end element.

This often means two loops can be used to solve the problem.
The outer loop is used to traverse the array. At each iteration, an index should be pointed to the start of the current range.
The inner loop is used to find the end of the current range.
At the end of each iteration, add the current range to the result list.

#### Code

Here is a sample solution.

```java
class Solution {
    public List<String> summaryRanges(int[] nums) {
        List<String> res = new ArrayList();
        int i=0;
        while(i<nums.length) {
            // when entering this loop
            // i is always at the starting of a range
            int s=i;

            // find the start of the next range
            while(i<nums.length && nums[i]-nums[s] == i-s) i++;

            if(s==i-1) res.add(""+nums[s]);
            else res.add(nums[s] + "->" + nums[i-1]);
        }

        return res;
    }
}
```

## Performance

The outer loop traverses each range in the array. The inner loop traverses each element in a range. So each element in the array is visited once. Therefore, the overall performance of the solution is O(n). No extra memory space is used in the solution.
