---
layout:     post
title:      "Problem: Palindrome Permutation II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
---

## Question

Given a string s, return all the palindromic permutations (without duplicates) of it. Return an empty list if no palindromic permutation could be form.

For example:

Given `s = "aabb"`, return `["abba", "baab"]`.

Given `s = "abc"`, return `[]`.

## Solution
TODO

#### Code
```java
class Solution {
    public List<String> generatePalindromes(String s) {
        List<String> results = new ArrayList<>();
        char[] chars = s.toCharArray();
        int[] charCount = new int[256];
        
        // count the appearance of each char
        for(char c: chars) {
            charCount[c]++;
        }
        
        // get the single char
        List<Character> halfChars = new ArrayList();
        Character single = null;
        for(int i=0; i<256; i++) {
            int count = charCount[i];
            if(count == 0) continue;
            if(count % 2 != 0) {
                if(single != null) return results;
                single = (char)i;
            }
            for(int j=0; j<count/2; j++) {
                halfChars.add((char)i);
            }
        }
        
        if(halfChars.isEmpty() && single != null) {
            results.add(new String(single+""));
            return results;
        }
        
        // depth first search to collect permutations
        List<String> halfPermutations = new ArrayList<>();
        dfsCollecthalfPermutations(halfChars.toArray(new Character[halfChars.size()]), halfPermutations, 0);
        
        // complete all the palindromic permutations
        for(String hp: halfPermutations) {
            StringBuilder sb = new StringBuilder(hp);
            if(single != null) {
                sb.append(single);
            }
            for(int i=hp.length()-1; i>=0; i--) {
                sb.append(hp.charAt(i));
            }
            results.add(sb.toString());
        }
        
        return results;
    }
        
    void dfsCollecthalfPermutations(Character[] chars, List<String> results, int index) {
        if(index == chars.length-1) {
            StringBuilder sb = new StringBuilder();
            for(Character c: chars) {
                sb.append(c);
            }
            results.add(sb.toString());
            return;
        }
        
        boolean[] set = new boolean[256];
        for(int i=index; i<chars.length; i++) {
            // aviud duplicate
            if(set[chars[i]]) continue;
            set[chars[i]] = true;
            swap(chars, index,i);
            dfsCollecthalfPermutations(chars, results, index+1);
            swap(chars, index, i);
        }
    }
    
    void swap(Character[] chars, int idx1, int idx2) {
        char c = chars[idx1];
        chars[idx1] = chars[idx2];
        chars[idx2] = c;
    }
}
```

## Performance
TODO