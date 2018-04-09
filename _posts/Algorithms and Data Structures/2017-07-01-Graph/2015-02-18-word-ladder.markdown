---
layout:     post
title:      "Problem: Word Ladder"
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

In this problem, we could construct a directed graph based on the wordList.

- Each node in the graph represents a word.
- Each edge from `A` to `B` represents that the word in `B` can be transformed from `A`.

Then the problem can be translated to: Given the graph, find the length of the shortest path from `beginWord` to `endWord`.

Finding the shortest path can be resolved by the **Breadth First Search (BFS)** algorithm. However, to find the length of the shortest path, we need to modify the standard BFS slightly. Please check the comment in the code for details.

#### Get Adjacent Words of a Node

There are different ways to achieve this. One way is to traverse each node in the list and collect the words if they are adjacent. To check if two words are adjacent, we need to compare the two words letter by letter. If the word list has `n` words and each word has `l` letters, the time complexity will be `O(n x l)`.

A more efficient way to do this is by changing each letter of the source node from `a` to `z`, and see if the result word is in the word list. If we construct the word list to a set initially, search the transformed word in the word set is an `O(1)` operation. And the overall time complexity becomes `O(26 x l) x O(1) = O(l)`. The following code uses this method.

Every time we reach a node, we need to remove it from the list to make sure we won't come back to the word again if the word is adjacent to a farther word.

#### Code

Here is a sample solution.

```java
class Solution {
    public int ladderLength(String beginWord, String endWord, List<String> wordList) {
        Set<String> wordSet = new HashSet<String>(wordList);
        Queue<String> q = new LinkedList();
        q.add(beginWord);

        int distance = 1;
        while(!q.isEmpty()) {
            distance ++;
            int size = q.size();

            // Make sure all the nodes in the queue now
            // have the same distance, to the beginWord node.
            // Traverse all the nodes of the current level,
            // add their next adjacent nodes to the queue. After
            // the loop, all the nodes will be distance+1 steps
            // from beginWord
            for(int i=1; i<=size; i++) {
                String w = q.poll();
                List<String> adjacentWords = getAdjacentWords(w, wordSet);
                for(String adjWord : adjacentWords) {
                    wordSet.remove(adjWord);
                    if(adjWord.equals(endWord)) return distance;
                    q.add(adjWord);
                }
            }
        }

        return 0;
    }

    private List<String> getAdjacentWords(String word, Set wordSet) {
        List<String> adjWords = new ArrayList<String>();
        char[] chars = word.toCharArray();
        for(int i=0; i<chars.length; i++) {
            char origin = chars[i];
            for(char c='a'; c<='z'; c++) {
                if(c == origin) continue;
                chars[i] = c;
                String adjWord = String.valueOf(chars);
                if(wordSet.contains(adjWord)) {
                    adjWords.add(adjWord);
                }
            }
            chars[i] = origin;
        }

        return adjWords;
    }
}
```

## Performance

Suppose we have `n` words in the graph. For the **BFS**, the time complexity is `O(n)`. Looking up for the adjacent nodes for each node is an `O(l)` operation. So the overrall complexity is `O(n*l)`.
