---
layout:     post
title:      "Problem: Valid Parenthesis String"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Medium
---

## Question

Given a string containing only three types of characters: '(', ')' and '*', write a function to check whether this string is valid. We define the validity of a string by these rules:

- Any left parenthesis '(' must have a corresponding right parenthesis ')'.
- Any right parenthesis ')' must have a corresponding left parenthesis '('.
- Left parenthesis '(' must go before the corresponding right parenthesis ')'.
- '*' could be treated as a single right parenthesis ')' or a single left parenthesis '(' or an empty string.
- An empty string is also valid.

```
Example 1:
Input: "()"
Output: True
Example 2:
Input: "(*)"
Output: True
Example 3:
Input: "(*))"
Output: True
```


## Solution
TODO

#### Code
```java
class Solution {
    public boolean checkValidString(String s) {
        return check(s, 0, 0, 0);
    }

    public boolean check(String s, int i, int l, int r) {
        if(r > l) return false;
        if(i == s.length()) {
            if(l == r) return true;
            return false;
        }
        char c = s.charAt(i);
        if(c == '(') return check(s, i+1, l+1, r);
        else if(c==')') return check(s, i+1, l, r+1);
        else {
            return check(s, i+1, l+1, r) || check(s, i+1, l, r+1) || check(s, i+1, l, r);
        }
    }
}
```

## Performance
TODO
