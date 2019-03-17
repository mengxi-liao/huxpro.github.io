---
layout:     post
title:      "Problem: Wiggle Sort"
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

Given an unsorted array nums, reorder it in-place such that
```
nums[0] <= nums[1] >= nums[2] <= nums[3]....
```

**Example:**
```
Input: nums = [3,5,2,1,6,4]
Output: One possible answer is [3,5,1,6,2,4]
```


#### Code
```java
class Solution {
    public void wiggleSort(int[] nums) {
        for(int i=1; i<nums.length; i++) {
            if(i%2 == 1 && nums[i] < nums[i-1]) {
                swap(nums, i, i-1);
            }
            else if(i%2 == 0 && nums[i] > nums[i-1]) {
                swap(nums, i, i-1);
            }
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
O(n)
