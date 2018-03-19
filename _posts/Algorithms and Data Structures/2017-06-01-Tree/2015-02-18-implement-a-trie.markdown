---
layout:     post
title:      "An Easy Way to Understand Algorithm Complexity and Big O Notation"
date:       2017-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Lesson
    - Algorithms and Data Structures
    - Trie
---

# Solution

TODO

# Code

```java
class TrieNode {
    // Initialize your data structure here.
    private TrieNode [] records;
    private boolean isEnd;

    public TrieNode() {
        records = new TrieNode[26];
    }

    public void setIsEnd() {
        isEnd = true;
    }

    public boolean isEnd() {
        return isEnd;
    }

    public TrieNode getRecord(char c) {
        return records[c-'a'];
    }

    public void setRecord(char c, TrieNode node) {
        records[c-'a'] = node;
    }
}

public class Trie {
    private TrieNode root;

    public Trie() {
        root = new TrieNode();
    }

    // Inserts a word into the trie.
    public void insert(String word) {
        TrieNode current = root;
        int i = 0;
        while(i<word.length() && current.getRecord(word.charAt(i))!=null) {
            current = current.getRecord(word.charAt(i));
            i ++;
        }
        if(i==word.length()) {
            current.setIsEnd();
            return;
        }
        while(i<word.length()) {
            TrieNode newNode = new TrieNode();
            current.setRecord(word.charAt(i), newNode);
            current = newNode;
            i ++;
        }
        current.setIsEnd();
        return;
    }

    // Returns if the word is in the trie.
    public boolean search(String word) {
        TrieNode current = root;
        int i = 0;
        while(i<word.length() && current.getRecord(word.charAt(i))!=null) {
            current = current.getRecord(word.charAt(i));
            i ++;
        }
        if(i==word.length() && current.isEnd()) return true;
        else return false;
    }

    // Returns if there is any word in the trie
    // that starts with the given prefix.
    public boolean startsWith(String prefix) {
        TrieNode current = root;
        int i = 0;
        while(i<prefix.length() && current.getRecord(prefix.charAt(i))!=null) {
            current = current.getRecord(prefix.charAt(i));
            i ++;
        }
        if(i==prefix.length()) return true;
        else return false;
    }
}
```