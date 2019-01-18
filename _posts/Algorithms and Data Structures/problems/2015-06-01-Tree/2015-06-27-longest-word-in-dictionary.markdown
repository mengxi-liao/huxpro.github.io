---
layout:     post
title:      "Problem: Longest Word in Dictionary"
date:       2017-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Lesson
    - Algorithms and Data Structures
    - Trie
    - Medium
---

## Question

Given a list of strings words representing an English Dictionary, find the longest word in words that can be built one character at a time by other words in words. If there is more than one possible answer, return the longest word with the smallest lexicographical order.

If there is no answer, return the empty string.
**Example 1:**
```
Input: 
words = ["w","wo","wor","worl", "world"]
Output: "world"
Explanation: 
The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
```
**Example 2:**
```
Input: 
words = ["a", "banana", "app", "appl", "ap", "apply", "apple"]
Output: "apple"
Explanation: 
Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".
```

## Solution

TODO

## Code

```java
class Solution {
    class TrieNode {
        TrieNode parent;
        char c;
        TrieNode[] children = new TrieNode[26];
        String word = null;
    }
    
    class Trie {
        TrieNode root = new TrieNode();
        
        public void insert(String w) {
            TrieNode current = root;
            for(int i=0; i<w.length(); i++) {
                char c = w.charAt(i);
                TrieNode node = current.children[c-'a'];
                if(node == null) {
                    node = new TrieNode();
                    node.c = c;
                    current.children[c-'a'] = node;
                }
                current = node;
            }
            current.word = w;
        }
    }
    
    public String longestWord(String[] words) {
        Trie trie = new Trie();
        for(String w:words) trie.insert(w);
        Map<Integer, String> levelWordMap = new HashMap<>();
        dfs(trie.root, levelWordMap, 0);
        int max = 0;
        for(int level:levelWordMap.keySet()) max = Math.max(level, max);
        return levelWordMap.get(max);
    }
    
    public void dfs(TrieNode root, Map<Integer, String> levelWordMap, int level) {
        for(int i=0; i<26; i++) {
            TrieNode n = root.children[i];
            if(n != null && n.word != null) {
                if(!levelWordMap.containsKey(level+1)) levelWordMap.put(level+1, n.word);
                dfs(n, levelWordMap, level+1);
            }
        }
    }
}
```
