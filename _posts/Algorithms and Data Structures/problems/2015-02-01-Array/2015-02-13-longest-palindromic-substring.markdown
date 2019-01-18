---
layout:     post
title:      "Problem: Longest Palindromic Substring"
date:       2015-02-13 00:00:00
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

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

**Example 1:**

```
Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
```

**Example 2:**

```
Input: "cbbd"
Output: "bb"
```

## Solution

TODO

#### Code

Here is a sample solution.

```java
class Solution {
    public String longestPalindrome(String s) {
        if(s.length() == 0) return s;
        int[] l = new int[] {0, 0};
        for(int i=0; i<s.length(); i++) {
            int[] p1 = expand(s, i, i);
            int[] p2 = expand(s, i-1, i);
            if(p1[1] - p1[0] > l[1] - l[0]) l = p1;
            if(p2[1] - p2[0] > l[1] - l[0]) l = p2;
        }

        return s.substring(l[0], l[1]+1);
    }

    private int[] expand(String s, int i1, int i2) {
        while(i1 >= 0 && i2 < s.length() && s.charAt(i1) == s.charAt(i2)) {
            i1--;
            i2++;
        }

        return new int[]{i1+1, i2-1};
    }
}
```

## Performance
`O(n^2)`
