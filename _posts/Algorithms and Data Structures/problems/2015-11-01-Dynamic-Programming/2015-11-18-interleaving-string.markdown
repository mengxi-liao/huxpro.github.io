---
layout:     post
title:      "Problem: Interleaving String"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Dynamic Programming
    - Depth First Search
    - Hard
---

## Question

Given s1, s2, s3, find whether s3 is formed by the interleaving of s1 and s2.

**Example 1:**
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbcbcac"
Output: true
```

**Example 2:**
```
Input: s1 = "aabcc", s2 = "dbbca", s3 = "aadbbbaccc"
Output: false
```

## Solution
Dynamic Programming

#### Code
```java
class Solution {
    public boolean isInterleave(String s1, String s2, String s3) {
        if(s1.length() + s2.length() != s3.length()) return false;
        boolean[][] cache = new boolean[s1.length()+1][s2.length()+1];
        cache[0][0] = true;
        for(int i=1; i<=s1.length(); i++)
            cache[i][0] = cache[i-1][0] && s3.charAt(i-1) == s1.charAt(i-1);
        for(int j=1; j<=s2.length(); j++)
            cache[0][j] = cache[0][j-1] && s3.charAt(j-1) == s2.charAt(j-1);

        for(int i=1; i<=s1.length(); i++) {
            for(int j=1; j<=s2.length(); j++) {
                cache[i][j] = (cache[i-1][j] && s3.charAt(i+j-1) == s1.charAt(i-1)) ||
                              (cache[i][j-1] && s3.charAt(i+j-1) == s2.charAt(j-1));
            }
        }
        return cache[s1.length()][s2.length()];
    }
}
```

#### Performance
O(s1.length*s2.length)
