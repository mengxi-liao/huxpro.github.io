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
        return restore(s, 4);
    }

    public List<String> restore(String s, int num) {
        List<String> results = new ArrayList<>();
        if(s.length() == 0 || s.length() > num*3) return results;
        if(num == 1 && validDigits(s)) {
            results.add(s);
            return results;
        }
        for(int i=1; i<=3; i++) {
            if(s.length() < i) break;
            String head = s.substring(0,i);
            if(!validDigits(head)) continue;
            List<String> subResults = restore(s.substring(i),num-1);
            for(String sub:subResults) {
                results.add(head+"."+sub);
            }
        }
        return results;
    }

    private boolean validDigits(String digits) {
        if(digits.charAt(0) == '0' && digits.length() > 1) return false;
        if(digits.length() > 3) return false;
        int v = Integer.valueOf(digits);
        return v <= 255 && v >= 0;
    }
}
```
