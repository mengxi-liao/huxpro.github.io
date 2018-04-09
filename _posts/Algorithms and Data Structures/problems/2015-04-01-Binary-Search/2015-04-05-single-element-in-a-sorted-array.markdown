---
layout:     post
title:      "Problem: Single Element in a Sorted Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Binary Search
    - Medium
---

## Question

Given a sorted array consisting of only integers where every element appears twice except for one element which appears once. Find this single element that appears only once.

**Example 1:**
```
Input: [1,1,2,3,3,4,4,8,8]
Output: 2
```

**Example 2:**
```
Input: [3,3,7,7,10,11,11]
Output: 10
```

**Note:** Your solution should run in O(log n) time and O(1) space.

## Solution
TODO

#### Code
```java
class Solution {
    public int singleNonDuplicate(int[] nums) {
        if(nums.length == 1) return nums[0];
        int l = 0;
        int r = nums.length - 1;
        while(l < r) {
            int m = l + (r-l)/2;
            if(m%2 == 1) m--;
            if(nums[m] == nums[m+1]) l = m+2;
            else r = m;
        }
        
        return nums[l];
    }
}

class Solution {
    public int singleNonDuplicate(int[] nums) {
        int l=0;
        int r = nums.length-1;
        while(l < r) {
            int mid = (l + r) / 2;
            if(mid % 2 == 0) {
                // if the leftside excluding mid has 
                // no single element, mid should be a new number
                if(nums[mid] == nums[mid+1]) {
                    // mid is a new number, leftside has no single number
                    // select the right side
                    l = mid+2;
                }
                else {
                    // mid is not a new number, select the left side
                    r = mid;
                }
            }
            else {
                // if the leftside including mid has 
                // no single element, mid should be an old number
                if(nums[mid] == nums[mid-1]) {
                    // mid is an old number, select the right side
                    l = mid + 1;
                }
                else {
                    // mid is a new number, select the left side
                    r = mid - 1;
                }
            }
        }
            
        return nums[l];
    }
}
```

## Performance
TODO
