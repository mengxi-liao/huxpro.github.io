---
layout:     post
title:      "Problem: Word Ladder II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Breadth First Search
    - Medium
---

## Question

Given two words (beginWord and endWord), and a dictionary's word list, find the length of shortest transformation sequence from beginWord to endWord, such that:

- Only one letter can be changed at a time.
- Each transformed word must exist in the word list. Note that beginWord is not a transformed word.

For example,

Given:
beginWord = `"hit"`
endWord = `"cog"`
wordList = `["hot","dot","dog","lot","log","cog"]`
As one shortest transformation is `"hit" -> "hot" -> "dot" -> "dog" -> "cog"`,
return its length `5`.

Note:
- Return 0 if there is no such transformation sequence.
- All words have the same length.
- All words contain only lowercase alphabetic characters.
- You may assume no duplicates in the word list.
- You may assume beginWord and endWord are non-empty and are not the same.

## Solution

Use the same BFS algorithms used in Word Ladder to get the distance of each nodes in the path from `beginWord` to `endWord`. Then use DFS backtracing to rebuild the paths.

#### Code

Here is a sample solution.

```java
class Solution {
    public List<List<String>> findLadders(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<>(wordList);
        wordSet.add(beginWord);
        Map<String, Integer> levels = new HashMap<>();
        Map<String, List<String>> adjCache = new HashMap<>();
        Queue<String> q = new LinkedList<>();
        q.add(beginWord);
        levels.put(beginWord, 0);
        int level = 0;
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i=0; i<size; i++) {
                String w = q.poll();
                List<String> children = getAdjacents(w, wordSet, adjCache);
                for(String c:children) {
                    if(levels.containsKey(c)) continue;
                    q.offer(c);
                    levels.put(c, level+1);
                }
            }

            if(levels.containsKey(endWord)) {
                List<List<String>> results = new ArrayList<>();
                List<String> result = new ArrayList<String>();
                result.add(0, endWord);
                buildResults(levels, beginWord, results, result, wordSet, adjCache);
                return results;
            }
            level ++;
        }

        return new ArrayList<List<String>>();
    }

    private void buildResults(
        Map<String, Integer> levels,
        String beginWord,
        List<List<String>> results,
        List<String> result,
        Set<String> wordSet,
        Map<String, List<String>> adjCache
    ) {
        String head = result.get(0);
        if(beginWord.equals(head)) {
            results.add(new ArrayList<String>(result));
            return;
        }

        int level = levels.get(head);
        List<String> adjs = getAdjacents(head, wordSet, adjCache);
        for(String adj: adjs) {
            if(levels.containsKey(adj) && levels.get(adj) == level-1) {
                result.add(0,adj);
                buildResults(levels, beginWord, results, result, wordSet, adjCache);
                result.remove(0);
            }
        }
    }

    private List<String> getAdjacents(
        String w,
        Set<String> wordSet,
        Map<String, List<String>> cache
    ) {
        if(cache.containsKey(w)) return cache.get(w);
        char[] chars = w.toCharArray();
        List<String> results = new ArrayList<String>();
        for(int i=0; i<chars.length; i++) {
            char o = chars[i];
            for(char c='a'; c<='z'; c++) {
                chars[i] = c;
                String s = new String(chars);
                if(wordSet.contains(s)) {
                    results.add(s);
                }
            }
            chars[i] = o;
        }
        cache.put(w, results);
        return results;
    }
}
```

## Performance

TODO
