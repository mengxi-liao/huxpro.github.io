---
layout:     post
title:      "Problem: Find All Anagrams in a String"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Medium
---

## Question

Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p will not be larger than 20,100.

The order of output does not matter.

**Example 1:**

```
Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
```

**Example 2:**

```
Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```

## Solution
TODO

#### Code
```java
class Solution {
    public List<Integer> findAnagrams(String s, String p) {
        List<Integer> result = new ArrayList<>();
        int[] hash = new int[26];
        int[] hashP = new int[26];
        for(int i=0; i<p.length(); i++) hashP[p.charAt(i) - 'a'] ++;
        for(int endIdx = 0; endIdx<s.length(); endIdx ++) {
            hash[s.charAt(endIdx) - 'a'] ++;
            int startIdx = endIdx - p.length() + 1;
            if(startIdx > 0) hash[s.charAt(startIdx-1) - 'a'] --;
            if(compare(hash, hashP)) result.add(startIdx);
        }
        
        return result;
    }
    
    private boolean compare(int[] h1, int[] h2) {
        for(int i=0; i<h1.length; i++) {
            if(h1[i] != h2[i]) return false;
        }
        return true;
    }
}
```

## Performance
TODO
