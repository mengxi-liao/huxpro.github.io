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

## Solution 1
Depth first search

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

## Solution 2
This Solution use 2D DP. beat 90% solutions, very simple.

Here are some conditions to figure out, then the logic can be very straightforward.

```
1, If p.charAt(j) == s.charAt(i) :  dp[i][j] = dp[i-1][j-1];
2, If p.charAt(j) == '.' : dp[i][j] = dp[i-1][j-1];
3, If p.charAt(j) == '*':
   here are two sub conditions:
               1   if p.charAt(j-1) != s.charAt(i) : dp[i][j] = dp[i][j-2]  //in this case, a* only counts as empty
               2   if p.charAt(i-1) == s.charAt(i) or p.charAt(i-1) == '.':
                              dp[i][j] = dp[i-1][j]    //in this case, a* counts as multiple a
                           or dp[i][j] = dp[i][j-1]   // in this case, a* counts as single a
                           or dp[i][j] = dp[i][j-2]   // in this case, a* counts as empty
```

#### Code
```java
class Solution {
    public boolean isMatch(String s, String p) {
        boolean[][] cache = new boolean[s.length()+1][p.length()+1];
        cache[0][0] = true;
        for(int i=1; i<=p.length(); i++) {
            if(p.charAt(i-1) == '*')
                cache[0][i] = cache[0][i-2];
        }

        for(int i=1; i<=s.length(); i++) {
            for(int j=1; j<=p.length(); j++) {
                if(p.charAt(j-1) == s.charAt(i-1) || p.charAt(j-1) == '.') {
                    cache[i][j] = cache[i-1][j-1];
                }
                else if(p.charAt(j-1) == '*') {
                    if(p.charAt(j-2) == s.charAt(i-1) || p.charAt(j-2) == '.') {
                        cache[i][j] = (cache[i-1][j] || cache[i][j-1]);
                    }
                    cache[i][j] ||= cache[i][j-2];
                }
            }
        }

        return cache[s.length()][p.length()];
    }
}
```


## Performance
TODO
