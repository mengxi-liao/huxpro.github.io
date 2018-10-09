---
layout:     post
title:      "Problem: Valid Anagram"
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
    - Easy
---

## Question

Given two strings s and t, write a function to determine if t is an anagram of s.

For example,
s = `"anagram"`, t = `"nagaram"`, return `true`.
s = `"rat"`, t = `"car"`, return `false`.

**Note:**
You may assume the string contains only lowercase alphabets.

**Follow up:**
What if the inputs contain unicode characters? How would you adapt your solution to such case?

## Solution
TODO

#### Code
```java
class Solution {
    public boolean isAnagram(String s, String t) {
        if(s.length() != t.length()) return false;
        
        Map<Character, Integer> charCount = new HashMap();
        for(int i=0; i<s.length(); i++) {
            Character c = s.charAt(i);
            if(!charCount.containsKey(c))
                charCount.put(c, 0);
            int count = charCount.get(c);
            charCount.put(c, count+1);
        }
        
        for(int i=0; i<t.length(); i++) {
            Character c = t.charAt(i);
            if(!charCount.containsKey(c) || charCount.get(c) == 0) return false;
            int count = charCount.get(c);
            charCount.put(c, count-1);
        }
        
        return true;
    }
}
```

## Performance
TODO
