---
layout:     post
title:      "Problem: Restore IP Addresses"
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

Given a string containing only digits, restore it by returning all possible valid IP address combinations.

**For example:**

Input: `"25525511135"`

Output: `["255.255.11.135", "255.255.111.35"]`

## Solution
Use backtracing. Each level constructs a part of the IP, and continue to search the following parts.

Be careful to the edge case
- When there is only 1 part left, add the left part in the results if all the left digits is a valid part, otherwise return empty results.
- When there is not enough digits, return empty results.

#### Code
```java
class Solution {
    public List<String> restoreIpAddresses(String s) {
        return build(s, 0, 4);
    }

    public List<String> build(String s, int start, int parts) {
        List<String> results = new ArrayList();
        if(start >= s.length()) return results;
        if(parts == 1) {
            String leftPart = s.substring(start, s.length());
            if(validPart(leftPart)) {
                results.add(leftPart);
            }
            return results;
        }

        for(int i=start; i<start + 3 && i<s.length(); i++) {
            String part = s.substring(start, i+1);
            if(validPart(part)) {
                List<String>followingParts = build(s, i+1, parts - 1);
                for(String follow : followingParts) {
                    results.add(part + '.' + follow);
                }
            }
        }

        return results;
    }

    public boolean validPart(String part) {
        if(part.charAt(0) == '0' && part.length() > 1) return false;
        if(part.length() > 3) return false;
        int v = Integer.valueOf(part);
        return v <= 255 && v >= 0;
    }
}
```
