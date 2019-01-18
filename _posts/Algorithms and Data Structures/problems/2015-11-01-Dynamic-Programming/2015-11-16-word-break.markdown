---
layout:     post
title:      "Problem: Word Break"
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
    - Medium
---

## Question

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

The same word in the dictionary may be reused multiple times in the segmentation.
You may assume the dictionary does not contain duplicate words.

**Example 1:**

```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```

**Example 2:**

```
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```

**Example 3:**

```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```


## Solution
TODO

#### Code
```java
class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        boolean[] cache = new boolean[s.length()+1];
        cache[0] = true;
        for(int i=1; i<=s.length(); i++) {
            int si = i-1;
            for(String w:wordDict) {
                int start = si - w.length() + 1;
                if(start < 0) continue;
                int end = si;
                String w2 = s.substring(start, end+1);
                if(w.equals(w2) && cache[start]) {
                    cache[i] = true;
                    break;
                }
            }
        }

        return cache[s.length()];
    }
}
```

## Performance
TODO
