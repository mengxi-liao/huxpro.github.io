---
layout:     post
title:      "Problem: Evaluate Reverse Polish Notation"
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

Evaluate the value of an arithmetic expression in Reverse Polish Notation.

Valid operators are `+, -, *, /`. Each operand may be an integer or another expression.

Some examples:
```
  ["2", "1", "+", "3", "*"] -> ((2 + 1) * 3) -> 9
  ["4", "13", "5", "/", "+"] -> (4 + (13 / 5)) -> 6
```

## Solution
TODO

#### Code
```java
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack();
        for(String token : tokens) {
            if(token.equals("+")) {
                int v2 = stack.pop();
                int v1 = stack.pop();
                stack.push(v1+v2);
            }
            else if (token.equals("-")) {
                int v2 = stack.pop();
                int v1 = stack.pop();
                stack.push(v1-v2);
            }
            else if (token.equals("*")) {
                int v2 = stack.pop();
                int v1 = stack.pop();
                stack.push(v1*v2);
            }
            else if (token.equals("/")) {
                int v2 = stack.pop();
                int v1 = stack.pop();
                stack.push(v1/v2);
            }
            else {
                stack.push(Integer.valueOf(token));
            }
        }
        
        return stack.peek();
    }
}
```

## Performance
TODO
