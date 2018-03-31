---
layout:     post
title:      "Problem: Generate Parentheses"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Medium
---

## Question

Given n pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

For example, given n = 3, a solution set is:

```
[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```


## Solution
TODO

#### Code
```java
class Solution {
    public List<String> generateParenthesis(int n) {
        int l = n;
        int r = n;
        List<String> results = new ArrayList();
        StringBuilder sb = new StringBuilder();
        collect(results, l, r, sb);
        
        return results;
    }
    
    private void collect(List<String> results, int l, int r, StringBuilder sb) {
        if(r==0) {
            results.add(sb.toString());    
            return;
        }
        
        if(l>0) {
            sb.append("(");
            collect(results, l-1, r, sb);
            sb.deleteCharAt(sb.length()-1);
        }
        
        if(l<r) {
            sb.append(")");
            collect(results, l, r-1, sb);
            sb.deleteCharAt(sb.length()-1);
        } 
    }
}
```

## Performance
TODO
