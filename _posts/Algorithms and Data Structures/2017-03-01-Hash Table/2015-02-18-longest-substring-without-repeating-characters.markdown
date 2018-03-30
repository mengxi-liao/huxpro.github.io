---
layout:     post
title:      "Problem: Longest Substring Without Repeating Characters"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
---

## Question

Given a string, find the length of the **longest substring** without repeating characters.

**Examples:**

Given `"abcabcbb"`, the answer is `"abc"`, which the length is 3.

Given `"bbbbb"`, the answer is `"b"`, with the length of 1.

Given `"pwwkew"`, the answer is `"wke"`, with the length of 3. Note that the answer must be a **substring**, `"pwke"` is a subsequence and not a substring.

## Solution
TODO

#### Code
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        Set<Character> set = new HashSet<>();
        int max = 0;
        for(int i=0; i<s.length(); i++) {
            char c = s.charAt(i);
            while(set.contains(c)) set.remove(s.charAt(i-set.size()));
            set.add(c);
            max = Math.max(max, set.size());
        }
        
        return max;
    }
}
```

## Performance
TODO