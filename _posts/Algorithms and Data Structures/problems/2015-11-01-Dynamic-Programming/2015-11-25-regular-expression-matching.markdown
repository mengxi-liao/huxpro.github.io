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
        Set<Integer> idxs = new HashSet<>();
        idxs.add(0);

        for(int i=0; i<p.length(); i++) {
            Set<Integer> idxsNew = new HashSet<>();
            char c = p.charAt(i);
            boolean multiple = false;
            if(i < p.length()-1 && p.charAt(i+1) == '*') {
                i++;
                multiple = true;
            }

            for(Integer index : idxs) {
                if(!multiple) {
                    if(c == '.' || index < s.length() && c == s.charAt(index)) {
                        idxsNew.add(index + 1);
                    }
                }
                else {
                    idxsNew.add(index);
                    for(int j = index+1; j <= s.length(); j++) {
                        if(c != '.' && s.charAt(j-1) != c) break;
                        idxsNew.add(j);
                    }
                }
            }

            if(idxsNew.isEmpty()) return false;
            idxs = idxsNew;
        }

        return idxs.contains(s.length());
    }
}
```

## Performance
TODO
