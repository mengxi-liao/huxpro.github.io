---
layout:     post
title:      "Problem: Word Search II"
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
    - Medium
---

## Question

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example:**

```
Input: 
words = ["oath","pea","eat","rain"] and board =
[
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]

Output: ["eat","oath"]
```

## Solution
TODO

#### Code
```java
class Solution {
    class TrieNode {
        char c;
        String word;
        TrieNode[] nexts;

        TrieNode() {
            word = null;
            nexts = new TrieNode[26];
        }

        TrieNode get(char c) {
            return nexts[c - 'a'];
        }

        TrieNode add(char c) {
            TrieNode node = new TrieNode();
            nexts[c - 'a'] = node;
            node.c = c;
            return node;
        }
    }

    public List<String> findWords(char[][] board, String[] words) {
        TrieNode root = BuildTrie(words);
        Set<String> results = new HashSet<>();
        for(int i=0; i<board.length; i++) {
            for(int j=0; j<board[0].length; j++) {
                List<String> res = new ArrayList<>();
                dfs(root, i, j, board, res);
                results.addAll(res);
            }
        }
        return new ArrayList<>(results);
    }

    public void dfs(TrieNode node, int i, int j, char[][] board, List<String> res) {
        if(i<0 || i>=board.length || j<0 || j>=board[0].length) return;
        if(board[i][j] == '0') return;
        TrieNode cur = node.get(board[i][j]);
        if(cur == null) return;
        if(cur.word != null) res.add(cur.word);
        char orgin = board[i][j];
        board[i][j] = '0';
        dfs(cur, i+1, j, board, res);
        dfs(cur, i-1, j, board, res);
        dfs(cur, i, j+1, board, res);
        dfs(cur, i, j-1, board, res);
        board[i][j] = orgin;
    }

    private TrieNode BuildTrie(String[] words) {
        TrieNode root = new TrieNode();
        for(String w: words) {
            TrieNode cur = root;
            for(int i=0; i<w.length(); i++) {
                char c = w.charAt(i);
                TrieNode next = cur.get(c);
                if(next == null) next = cur.add(c);
                cur = next;
            }
            cur.word = w;
        }

        return root;
    }
}
```

## Performance
TODO
