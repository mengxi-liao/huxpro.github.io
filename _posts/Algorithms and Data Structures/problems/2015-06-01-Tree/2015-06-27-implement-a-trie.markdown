---
layout:     post
title:      "Problem: Implement a Trie"
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

# Solution

TODO

# Code

```java
class Trie {
    class TrieNode {
        TrieNode[] nodes = new TrieNode[26];
        char c;
        boolean end;
    }
    
    TrieNode root = new TrieNode();
    
    /** Inserts a word into the trie. */
    public void insert(String word) {
        TrieNode current = root;
        for(int i=0; i<word.length(); i++) {
            char c = word.charAt(i);
            if(current.nodes[c - 'a'] != null) {
                current = current.nodes[c - 'a'];
            }
            else {
                TrieNode n = new TrieNode();
                n.c = c;
                current.nodes[c - 'a'] = n;
                current = n;
            } 
        }
        
        current.end = true;
    }
    
    /** Returns if the word is in the trie. */
    public boolean search(String word) {
        TrieNode current = root;
        for(int i=0; i<word.length(); i++) {
            char c = word.charAt(i);
            if(current.nodes[c-'a'] == null) return false;
            current = current.nodes[c-'a'];
        }
        
        return current.end;
    }
    
    /** Returns if there is any word in the trie that starts with the given prefix. */
    public boolean startsWith(String prefix) {
        TrieNode current = root;
        for(int i=0; i<prefix.length(); i++) {
            char c = prefix.charAt(i);
            if(current.nodes[c-'a'] == null) return false;
            current = current.nodes[c-'a'];
        }
        return true;
    }
}
```
