---
layout:     post
title:      "Problem: Next Greater Element I"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
    - Medium
---

## Question

You are given two arrays (without duplicates) nums1 and nums2 where nums1’s elements are subset of nums2. Find all the next greater numbers for nums1's elements in the corresponding places of nums2.

The Next Greater Number of a number x in nums1 is the first greater number to its right in nums2. If it does not exist, output -1 for this number.

**Example 1:**
```
Input: nums1 = [4,1,2], nums2 = [1,3,4,2].
Output: [-1,3,-1]
Explanation:
    For number 4 in the first array, you cannot find the next greater number for it in the second array, so output -1.
    For number 1 in the first array, the next greater number for it in the second array is 3.
    For number 2 in the first array, there is no next greater number for it in the second array, so output -1.
```


## Solution
TODO

#### Code
```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Map<Integer, Integer> nums1indecies = new HashMap<>();
        for(int i=0; i<nums1.length; i++) nums1indecies.put(nums1[i], i);
        int[] results = new int[nums1.length];
        Arrays.fill(results, -1);

        Stack<Integer> s = new Stack<>();
        for(int i=0; i<nums2.length; i++) {
            while(!s.isEmpty() && s.peek() < nums2[i]) {
                int top = s.pop();
                if(nums1indecies.containsKey(top)) {
                    results[nums1indecies.get(top)] = nums2[i];
                }
            }

            s.push(nums2[i]);
        }

        return results;
    }
}
```

## Performance
TODO
