---
layout:     post
title:      "Problem: Regular Expression Matching"
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
    - Hard
---

## Question

Implement regular expression matching with support for `'.'` and `'*'`.

```
'.' Matches any single character.
'*' Matches zero or more of the preceding element.

The matching should cover the entire input string (not partial).

The function prototype should be:
bool isMatch(const char *s, const char *p)

Some examples:
isMatch("aa","a") → false
isMatch("aa","aa") → true
isMatch("aaa","aa") → false
isMatch("aa", "a*") → true
isMatch("aa", ".*") → true
isMatch("ab", ".*") → true
isMatch("aab", "c*a*b") → true
```

## Solution
TODO

#### Code
```java
class Solution {
    public boolean isMatch(String s, String p) {
        List<String> patterns = new ArrayList();
        char[] pc = p.toCharArray();
        for(int i=0; i<p.length(); i++) {
            char c = pc[i];
            if(pc[i] != '*') {
                patterns.add(c+"");
            }
            else {
                int last = patterns.size()-1;
                patterns.set(patterns.size()-1, patterns.get(last)+"*");
            }
        }
        
        Set<Integer>[] matchs = new Set[patterns.size()+1];
        matchs[0] = new HashSet<Integer>();
        matchs[0].add(-1);
        
        char[] sc = s.toCharArray();
        for(int i=0; i<patterns.size(); i++) {
            
            // for matchs, i is previous, i+1 is current
            if(matchs[i].isEmpty()) return false;
            
            matchs[i+1] = new HashSet();
            String pat = patterns.get(i);
            char c = pat.charAt(0);
            for(Integer idx: matchs[i]) {
                if(pat.length() != 2) {
                    if(idx < s.length()-1 && (pat.equals(".") || sc[idx+1] == c)) {
                        matchs[i+1].add(idx+1);
                    }
                } else {
                    matchs[i+1].add(idx);
                    for(int j=idx+1; j<s.length() && (c == '.' || sc[j] == c); j++) {
                        matchs[i+1].add(j);
                    }
                }
            }
            
        }
        
        
        return matchs[matchs.length-1].contains(s.length()-1);
    }
}
```

## Performance
TODO
