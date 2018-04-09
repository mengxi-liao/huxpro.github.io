---
layout:     post
title:      "Problem: Power of Two"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Math
---

## Question

Given an integer, write a function to determine if it is a power of two.

## Solution
TODO

#### Code
```java
class Solution {
    public boolean isPowerOfTwo(int n) {
        if(n<=0) return false;
        if(n==1) return true;
        
        while(n>=2) {
            if(n%2 == 1) return false;
            n/=2;
        }
        
        return true;
    }
}
```

## Performance
TODO