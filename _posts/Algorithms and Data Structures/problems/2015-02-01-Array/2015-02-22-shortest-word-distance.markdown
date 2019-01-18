---
layout:     post
title:      "Problem: Shortest Word Distance"
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
    - Easy
---

## Question

Given a list of words and two words word1 and word2, return the shortest distance between these two words in the list.

**Example:**
Assume that words = ["practice", "makes", "perfect", "coding", "makes"].
```
Input: word1 = “coding”, word2 = “practice”
Output: 3
```
```
Input: word1 = "makes", word2 = "coding"
Output: 1
```

## Solution

TODO

#### Code

Here is a sample solution.

```java
class Solution {
    public int shortestDistance(String[] words, String word1, String word2) {
        int idx = -1;
        String word = null;
        int min = Integer.MAX_VALUE;
        for(int i=0; i<words.length; i++) {
            if(words[i].equals(word2) || words[i].equals(word1)) {
                if(word != null && !word.equals(words[i])) {
                    min = Math.min(min, i-idx);
                }
                
                idx = i;
                word = words[i];
            }
        }
        
        return min;
    }
}
```

## Performance

`O(n)`
