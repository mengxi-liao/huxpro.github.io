---
layout:     post
title:      "Problem: Multiply Strings"
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

Given two non-negative integers num1 and num2 represented as strings, return the product of num1 and num2.

**Note:**

- The length of both `num1` and `num2` is < 110.
- Both `num1` and `num2` contains only digits 0-9.
- Both `num1` and `num2` does not contain any leading zero.
- You must not use any built-in BigInteger library or convert the inputs to integer directly.


## Solution
TODO

#### Code
```java
class Solution {
    public String multiply(String num1, String num2) {
        int m = num1.length(), n = num2.length();
        int[] pos = new int[m + n];
        for(int i=m-1; i>=0; i--) {
            for(int j=n-1; j>=0; j--) {
                int mul = (num1.charAt(i) - '0') * (num2.charAt(j) - '0');
                
                int h = i+j;
                int l = i+j+1;
                
                // p[h]p[l] = mul + p[h]p[l]
                int sum = mul + pos[l];
                pos[h] += sum / 10;
                pos[l] = sum % 10;
            }
        }
        
        StringBuilder sb = new StringBuilder();
        for(int p : pos) if(!(sb.length() == 0 && p == 0)) sb.append(p);
        return sb.length() == 0 ? "0" : sb.toString();
    }
}

// 1，2
// 6，9

// i=1
// j=1
// p1 = 2
// p2 = 3
// 0 0 1 8
// i=1
// j=0
// p1 = 1
// p2 = 2
// 0 1 3 8
// i=0
// j=1
// p1 = 1
// p2 = 2
// 0 2 2 8
// i=0
// j=0
// 0 8 2 8

//   1 8
// 1 2
//   9 
// 6
```

## Performance
TODO