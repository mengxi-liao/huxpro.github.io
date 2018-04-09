---
layout:     post
title:      "Problem: Decode Ways"
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
---

## Question

A message containing letters from A-Z is being encoded to numbers using the following mapping:

```
'A' -> 1
'B' -> 2
...
'Z' -> 26
```

Given an encoded message containing digits, determine the total number of ways to decode it.

For example,
Given encoded message `"12"`, it could be decoded as `"AB"` (1 2) or `"L"` (12).

The number of ways decoding `"12"` is 2.

## Solution
TODO

#### Code
```java
class Solution {
    public int numDecodings(String s) {
        if(s.length() == 0 || s.charAt(0) == '0') return 0;
        int[] decodeWays = new int[s.length()+1];
        decodeWays[0] = 1;
        decodeWays[1] = 1;
        for(int i=1; i<s.length(); i++) {
            int ways = 0;
            if(s.charAt(i) != '0') ways += decodeWays[i];
            int val = Integer.valueOf(s.substring(i-1, i+1));
            if(val <= 26 && val >= 10) ways += decodeWays[i-1];
            if(ways == 0) return 0;
            decodeWays[i+1] = ways;
        }
        
        return decodeWays[s.length()];
    }
}
```

## Performance
TODO