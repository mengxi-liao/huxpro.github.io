---
layout:     post
title:      "Problem: Decode String"
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

Given an encoded string, return it's decoded string.

The encoding rule is: `k[encoded_string]`, where the encoded_string inside the square brackets is being repeated exactly k times. Note that k is guaranteed to be a positive integer.

You may assume that the input string is always valid; No extra white spaces, square brackets are well-formed, etc.

Furthermore, you may assume that the original data does not contain any digits and that digits are only for those repeat numbers, k. For example, there won't be input like 3a or 2[4].

```
Example:

s = "3[a]2[bc]", return "aaabcbc".
s = "3[a2[c]]", return "accaccacc".
s = "2[abc]3[cd]ef", return "abcabccdcdcdef".
```

## Solution
TODO

#### Code
```java
class Solution {
    public String decodeString(String s) {
        Queue<Character> q = new LinkedList<>();
        for(int i=0; i<s.length(); i++) q.add(s.charAt(i));

        return decode(q);
    }

    public String decode(Queue<Character> q) {
        StringBuilder s = new StringBuilder();
        while(!q.isEmpty()) {
            char c = q.poll();
            if((c >= 'a' && c <= 'z') || (c>='A' && c <= 'Z')) s.append(c);
            else if(c<='9' && c >= '0') {
                int num = (c - '0');
                while(q.peek() <= '9' && q.peek() >= '0') {
                    num = num*10 + (q.peek() - '0');
                    q.poll();
                }
                q.poll();
                String nested = decode(q);
                for(int i=1; i<=num; i++) {
                    s.append(nested);
                }
            }
            else if(c == ']') break;
        }
        return s.toString();
    }
}
```

## Performance
O(n)
