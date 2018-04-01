---
layout:     post
title:      "Problem: Valid Parenthese"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
    - Easy
---

## Question

Given a string containing just the characters `'(', ')', '{', '}', '['` and `']'`, determine if the input string is valid.

The brackets must close in the correct order, `"()"` and `"()[]{}"` are all valid but `"(]"` and `"([)]"` are not.

## Solution
TODO

#### Code
```java
class Solution {
    public boolean isValid(String s) {
        Stack<Character> st = new Stack();
        for(int i=0; i<s.length(); i++) {
            char c = s.charAt(i);
            if(isRight(c)) {
                if(st.isEmpty() || !match(st.peek(), c)) {
                    return false;
                }
                st.pop();
            }
            else {
                st.push(c);
            }
        }
        
        return st.isEmpty();
    }
    
    public boolean isRight(char paren) {
        return paren == ')' || paren == '}' || paren == ']';
    }
    
    public boolean match(char left, char right) {
        return left == '(' && right == ')'
            || left == '[' && right == ']'
            || left == '{' && right == '}';
    }
}
```

## Performance
TODO
