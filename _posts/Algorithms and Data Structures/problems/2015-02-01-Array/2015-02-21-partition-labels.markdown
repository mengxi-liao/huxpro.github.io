---
layout:     post
title:      "Problem: Partition Labels"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Two Pointers
    - Greedy
    - Medium
---

## Question

A string `S` of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

```
Example 1:
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

**Note:**
- `S` will have length in range `[1, 500]`.
- `S` will consist of lowercase letters (`'a'` to `'z'`) only.

## Solution

TODO

#### Code

Here is a sample solution.

```java
class Solution {
    public List<Integer> partitionLabels(String S) {
        int[] ends = new int[26];
        
        for(int i=0; i<S.length(); i++) {
            char c = S.charAt(i);
            ends[c-'a'] = i;
        }
        
        int start = 0;
        int end = ends[S.charAt(0)-'a'];
        List<Integer> results = new ArrayList();
        for(int i=0; i<S.length(); i++) {
            if(i > end) {
                results.add(end+1-start);
                start = i;
                end = ends[S.charAt(i)-'a'];
            }
            else if(ends[S.charAt(i)-'a'] > end) {
                end = ends[S.charAt(i)-'a'];
            }
        }
        results.add(end+1-start);
        
        return results;
    }
}
```

## Performance

O(n)
