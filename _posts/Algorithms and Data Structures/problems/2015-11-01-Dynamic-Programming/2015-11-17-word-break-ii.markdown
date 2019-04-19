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
        Set<String> wordSet = new HashSet<>();
        wordSet.addAll(wordDict);
        List<Integer>[] prevs = new List[s.length()+1];
        for(int i=0; i<prevs.length; i++) prevs[i] = new ArrayList<>();
        prevs[0].add(-1);
        for(int i=1; i<=s.length(); i++) {
            for(int j=0; j<i; j++) {
                if(prevs[j].size() >= 1 && wordSet.contains(s.substring(j, i))) {
                    prevs[i].add(j);
                }
            }
        }

        List<String> results = new ArrayList<>();
        List<String> res = new LinkedList<>();
        backtrace(s.length(), s, prevs, res, results);
        return results;
    }

    private void backtrace(int end, String s, List<Integer>[] prevs, List<String> res, List<String> results) {
        if(end == 0) {
            results.add(String.join(" ", res));
            return;
        }

        for(int i=0; i<prevs[end].size(); i++) {
            int start = prevs[end].get(i);
            res.add(0, s.substring(start, end));
            backtrace(start, s, prevs, res, results);
            res.remove(0);
        }
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
