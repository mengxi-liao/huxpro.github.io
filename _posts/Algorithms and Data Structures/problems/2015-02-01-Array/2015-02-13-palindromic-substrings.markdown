---
layout:     post
title:      "Problem: Palindromic Substrings"
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

Given a string, your task is to count how many palindromic substrings in this string.

The substrings with different start indexes or end indexes are counted as different substrings even they consist of same characters.

**Example 1:**
```
Input: "abc"
Output: 3
Explanation: Three palindromic strings: "a", "b", "c".
```

**Example 2:**
```
Input: "aaa"
Output: 6
Explanation: Six palindromic strings: "a", "a", "a", "aa", "aa", "aaa".
```

## Solution

TODO

#### Code

Here is a sample solution.

```java
class Solution {
    public int countSubstrings(String s) {
        if(s.length() == 0) return 0;
        int sum = 1;
        for(int i=1; i<s.length(); i++) {
            sum += expand(i, i, s);
            sum += expand(i-1, i, s);
        }
        return sum;
    }

    public int expand(int b, int e, String s) {
        int count = 0;
        while(b>=0 && e<s.length() && s.charAt(b) == s.charAt(e)) {
            count++;
            b--;
            e++;
        }

        return count;
    }
}
```

## Performance
`O(n^2)`
