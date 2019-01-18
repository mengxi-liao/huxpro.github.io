---
layout:     post
title:      "Problem: Word Break II"
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

Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, add spaces in s to construct a sentence where each word is a valid dictionary word. Return all such possible sentences.

**Note:**

- The same word in the dictionary may be reused multiple times in the segmentation.
- You may assume the dictionary does not contain duplicate words.

**Example 1:**
```
Input:
s = "catsanddog"
wordDict = ["cat", "cats", "and", "sand", "dog"]
Output:
[
  "cats and dog",
  "cat sand dog"
]
```

**Example 2:**
```
Input:
s = "pineapplepenapple"
wordDict = ["apple", "pen", "applepen", "pine", "pineapple"]
Output:
[
  "pine apple pen apple",
  "pineapple pen apple",
  "pine applepen apple"
]
Explanation: Note that you are allowed to reuse a dictionary word.
```

**Example 3:**
```
Input:
s = "catsandog"
wordDict = ["cats", "dog", "sand", "and", "cat"]
Output:
[]
```

## Solution I
Dynamic Programming + Backtracing + cache

#### Code
```java
class Solution {
    public List<String> wordBreak(String s, List<String> wordDict) {
        boolean[][] cache = new boolean[s.length()][wordDict.size()];
        for(int i=0; i<wordDict.size(); i++) {
            String w = wordDict.get(i);
            if(s.startsWith(w)) {
                cache[w.length()-1][i] = true;
            }
        }

        for(int i=1; i<s.length(); i++) {
            for(int j=0; j<wordDict.size(); j++) {
                String w = wordDict.get(j);
                int start = i-w.length()+1;
                if(start < 0) continue;
                int end = i;
                if(s.substring(start, end+1).equals(w)) cache[i][j] = true;
            }
        }

        return backtrace(cache, s, wordDict, s.length()-1);
    }

    // a cache to memorize prev results
    Map<Integer, List<String>> map = new HashMap<>();
    public List<String> backtrace(
        boolean[][] cache,
        String s,
        List<String> wordDict,
        int end) {

        if(map.containsKey(end)) return map.get(end);

        List<String> results = new ArrayList();

        for(int i=0; i<wordDict.size(); i++) {
            String w = wordDict.get(i);
            int start = end - w.length() + 1;
            if(start < 0) continue;
            if(start == 0 && s.startsWith(w)) {
                results.add(w);
            }
            else if(s.substring(start, end+1).equals(w)){
                List<String> prevResults = backtrace(cache, s, wordDict, end-w.length());
                for(String pw: prevResults) {
                    results.add(pw + " " + w);
                }
            }
        }
        map.put(end, results);
        return results;
    }
}
```

#### Performance
TODO

## Solution II
DFS + cache

#### Code
```java
class Solution {
    Map<String, List<String>> cache = new HashMap<>();
    public List<String> wordBreak(String s, List<String> wordDict) {
        if(cache.containsKey(s)) return cache.get(s);
        List<String> results = new ArrayList<>();
        if(s.length() == 0) results.add("");
        for(String w:wordDict) {
            if(s.startsWith(w)) {
                List<String> subResults = wordBreak(s.substring(w.length()), wordDict);
                for(String sr:subResults) {
                    if(sr.length()==0) results.add(w);
                    else results.add(w+" "+sr);
                }
            }
        }
        cache.put(s, results);
        return results;
    }
}
```

#### Performance
TODO
