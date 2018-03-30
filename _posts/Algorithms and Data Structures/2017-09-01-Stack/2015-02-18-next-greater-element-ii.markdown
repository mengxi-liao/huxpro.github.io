---
layout:     post
title:      "Problem: Next Greater Element II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
---

## Question

Given a circular array (the next element of the last element is the first element of the array), print the Next Greater Number for every element. The Next Greater Number of a number x is the first greater number to its traversing-order next in the array, which means you could search circularly to find its next greater number. If it doesn't exist, output -1 for this number.

**Example:**

```
Input: [1,2,1]
Output: [2,-1,2]
Explanation: The first 1's next greater number is 2; 
The number 2 can't find next greater number; 
The second 1's next greater number needs to search circularly, which is also 2.
```

## Solution
TODO

#### Code
```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        if(nums.length == 0) return nums;
        int len = nums.length;
        int[] results = new int[len];
        int[] s = new int[len];
        int top = 0;
        
        for(int i=0; i<len; ++i) {
            while(top!=0 && nums[s[top-1]] < nums[i])
                results[s[--top]] = nums[i];
            s[top++] = i;
        }
        
        for(int i=0; i<len; ++i) {
            while(top!=0 && nums[s[top-1]] < nums[i]) 
            results[s[--top]] = nums[i];
        }
        
        while(top!=0) results[s[--top]] = -1;
        
        return results;
    }
}
```

## Performance
TODO