---
layout:     post
title:      "Problem: Next Permutation"
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

Implement next permutation, which rearranges numbers into the lexicographically next greater permutation of numbers.

If such arrangement is not possible, it must rearrange it as the lowest possible order (ie, sorted in ascending order).

The replacement must be in-place and use only constant extra memory.

Here are some examples. Inputs are in the left-hand column and its corresponding outputs are in the right-hand column.

```
1,2,3 → 1,3,2
3,2,1 → 1,2,3
1,1,5 → 1,5,1
```

#### Code
```java
class Solution {
    public void nextPermutation(int[] nums) {
        // To find the next larger permutation. We need
        // We need to find a element in the array, and swap it
        // with a larger element that after it.
        // We need to pick the first element as high position
        // as possible to minimize the increased amount.
        // note that nums[second] must be larger than nums[first]

        // find the last element, nums[first] < nums[first+1] so we could
        // pick a element nums[second] that is larger than num[first] and
        // second > first.
        int first = -1;
        int minIndex = nums.length-1;
        for(int i=nums.length-1; i>=1; i--) {
            if(nums[i-1] < nums[i]){
                first = i-1;
                break;
            }

        }

        // if the whole array is decending, just 
        // reverse the whole array to be ascending
        if(first == -1) {
            reverse(nums, 0, nums.length-1);
            return;
        }

        // To minimize the increased amount, we need to select
        // the min element after nums[first] that is larger than
        // nums[first]
        int second = -1;
        for(int i=nums.length-1; i>=0; i--) {
            if(nums[i] > nums[first]) {
                second = i;
                break;
            }
        }

        // swap the two elements
        int t = nums[first];
        nums[first] = nums[second];
        nums[second] = t;

        // nums[first+1] .. nums[n-1] is still ascending.
        // We need to minimize this part so just reverse the
        // elements of this part.
        reverse(nums, first+1, nums.length-1);
    }

    public void reverse(int[] nums, int start, int end) {
        while(start < end) {
            int t = nums[end];
            nums[end] = nums[start];
            nums[start] = t;
            start ++;
            end --;
        }
    }
}
```

## Performance
O(n)

## Notes

A few important test cases:
```
[1,2,3] => [3,2,1]
[1] => [1]
[3,2,5,4,1] => [3,4,1,2,5]
```