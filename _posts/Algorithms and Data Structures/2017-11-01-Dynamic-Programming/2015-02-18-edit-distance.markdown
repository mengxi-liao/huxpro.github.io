---
layout:     post
title:      "Problem: Edit Distance"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Dynamic Programming
---

## Question

Given two words word1 and word2, find the minimum number of steps required to convert word1 to word2. (each operation is counted as 1 step.)

You have the following 3 operations permitted on a word:

a) Insert a character
b) Delete a character
c) Replace a character

## Solution
TODO

#### Code
```java
class Solution {
    public int minDistance(String word1, String word2) {
        int n = word1.length();
        int m = word2.length();
        
        int[][] distances = new int[n+1][m+1];
        
        for(int i=0; i<n+1; i++) {
            distances[i][0] = i;
        }
        for(int i=0; i<m+1; i++) {
            distances[0][i] = i;
        }
        
        for(int i=1; i<n+1; i++) {
            for(int j=1; j<m+1; j++) {
                if(word1.charAt(i-1) == word2.charAt(j-1)) {
                    distances[i][j] = distances[i-1][j-1];
                }
                else { 
                    int a = distances[i-1][j-1];
                    int b = distances[i][j-1];
                    int c = distances[i-1][j];

                    distances[i][j] = 1 + Math.min(a,Math.min(b,c));
                }
            }
        }
        
        return distances[n][m];
    }
}
```

## Performance
TODO