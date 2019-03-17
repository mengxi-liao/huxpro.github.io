---
layout:     post
title:      "Problem: Minimum Window Substring"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Hard
    - Array
---

## Question

Given a string S and a string T, find the minimum window in S which will contain all the characters in T in complexity O(n).

**Example:**
```
Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
```
**Note:**
- If there is no such window in S that covers all characters in T, return the empty string "".
- If there is such window, you are guaranteed that there will always be only one unique minimum window in S.
## Solution
TODO

#### Code
```java
class Solution {
    public String minWindow(String s, String t) {
        HashMap<Character, Integer> tMap = new HashMap<>();
        for(int i=0; i<t.length(); i++) {
            char c = t.charAt(i);
            tMap.put(c, tMap.getOrDefault(c,0)+1);
        }

        int start = 0;
        int end = 0;
        int min = Integer.MAX_VALUE;
        int minStart = 0;
        int minEnd = Integer.MAX_VALUE;
        int visited = 0;

        while(end < s.length()) {
            char c = s.charAt(end);
            if(tMap.containsKey(c)) {
                int count = tMap.get(c)-1;
                tMap.put(c, count);
                if(count == 0) visited++;
            }

            // keep the substring between start and end qualified.
            if(visited == tMap.size()) {
                char startChar = s.charAt(start);
                while(!tMap.containsKey(startChar) || tMap.get(startChar) < 0) {
                    if(tMap.containsKey(startChar)) {
                        tMap.put(startChar, tMap.get(startChar)+1);
                    }
                    start++;
                    startChar = s.charAt(start);
                }

                int length = end-start;

                if(length < min) {
                    min = length;
                    minStart = start;
                    minEnd = end;
                }
            }
            end++;
        }

        return min == Integer.MAX_VALUE? "" : s.substring(minStart, minEnd+1);
    }
}
```

## Performance
O(n)
