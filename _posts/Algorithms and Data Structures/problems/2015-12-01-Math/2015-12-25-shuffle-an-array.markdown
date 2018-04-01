---
layout:     post
title:      "Problem: Shuffle an Array"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Math
    - Medium
---

## Question

Shuffle a set of numbers without duplicates.

Example:
```
// Init an array with set 1, 2, and 3.
int[] nums = {1,2,3};
Solution solution = new Solution(nums);

// Shuffle the array [1,2,3] and return its result. Any permutation of [1,2,3] must equally likely to be returned.
solution.shuffle();

// Resets the array back to its original configuration [1,2,3].
solution.reset();

// Returns the random shuffling of array [1,2,3].
solution.shuffle();
```


## Solution
TODO

#### Code
```java
import java.util.Random;

public class Solution {
    private int[] nums;
    private Random random;

    public Solution(int[] nums) {
        this.nums = nums;
        random = new Random();
    }
    
    /** Resets the array to its original configuration and return it. */
    public int[] reset() {
        return nums;
    }
    
    /** Returns a random shuffling of the array. */
    public int[] shuffle() {
        if(nums == null) return null;
        
        int [] a = nums.clone();
        for(int i=0; i<a.length; i++) {
            int j = random.nextInt(i+1);
            int temp = a[i];
            a[i] = a[j];
            a[j] = temp;
        }
        
        return a;
    }
}
```

## Performance
TODO
