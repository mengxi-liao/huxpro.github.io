---
layout:     post
title:      "Problem: Longest Substring with At Most Two Distinct Characters"
date:       2015-02-13 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Given a string s , find the length of the longest substring t  that contains at most 2 distinct characters.

**Example 1:**
```
Input: "eceba"
Output: 3
Explanation: t is "ece" which its length is 3.
```

**Example 2:**
```
Input: "ccaabbb"
Output: 5
Explanation: t is "aabbb" which its length is 5.
```

## Solution

Two pointers + hashmap

#### Code

Here is a sample solution.

```java
class Solution {
    public int lengthOfLongestSubstringTwoDistinct(String s) {
        int start = 0;
        Map<Character, Integer> counter = new HashMap<>();
        int max = 0;
        for(int end=0; end<s.length(); end++) {
            char c = s.charAt(end);
            counter.put(c,counter.getOrDefault(c,0)+1);
            while(counter.keySet().size() > 2) {
                char c2 = s.charAt(start);
                int count = counter.get(c2);
                if(count == 1) {
                    counter.remove(c2);
                }
                else {
                    counter.put(c2, count-1);
                }
                start++;
            }
            max = Math.max(max, end - start + 1);
        }

        return max;
    }
}
```

## Performance
`O(n)`
