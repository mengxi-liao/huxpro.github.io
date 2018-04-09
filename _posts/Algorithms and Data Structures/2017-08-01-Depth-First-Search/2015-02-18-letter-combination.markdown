---
layout:     post
title:      "Problem: Letter Combinations of a Phone Number"
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
---

## Question

Given a digit string, return all possible letter combinations that the number could represent. A mapping of digit to letters (just like on the telephone buttons) is given below.

![](/img/posts/dsa/letter-combination.png)

Input:Digit string "23"

Output: `["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"]`.

## Solution
TODO

#### Code
```java
class Solution {
    public List<String> letterCombinations(String digits) {
        List<String> results = new ArrayList<String>();
        if(digits == null || digits.length()==0) return results;
        char[][] keyboard = {
            {'a', 'b', 'c'}, {'d', 'e', 'f'},
            {'g', 'h', 'i'}, {'j', 'k', 'l'}, {'m', 'n', 'o'},
            {'p','q', 'r', 's'}, {'t', 'u', 'v'}, {'w', 'x', 'y', 'z'}
        };
            
        collect(results, keyboard, digits, 0, new StringBuilder());
            
        return results;
    }
        
    private void collect(
      List<String> results, 
      char[][] keyboard, 
      String digits, 
      int idx, 
      StringBuilder sb
    ) {
        if(idx == digits.length()) {
            results.add(sb.toString());
            return;
        }
        char digit = digits.charAt(idx);
        char[] options = keyboard[digit-'2'];
        for(char opt : options) {
            sb.append(opt);
            collect(results, keyboard, digits, idx+1, sb);
            sb.deleteCharAt(sb.length()-1);
        }
    }
}
```

## Performance
TODO