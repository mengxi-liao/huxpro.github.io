---
layout:     post
title:      "Problem: Alien Dictionary"
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
    - Depth First Search
    - Hard
    - Topological Sort
---

## Question

There is a new alien language which uses the latin alphabet. However, the order among letters are unknown to you. You receive a list of non-empty words from the dictionary, where words are sorted lexicographically by the rules of this new language. Derive the order of letters in this language.

**Example 1:**
```
Input:
[
  "wrt",
  "wrf",
  "er",
  "ett",
  "rftt"
]

Output: "wertf"
```
**Example 2:**
```
Input:
[
  "z",
  "x"
]

Output: "zx"
```
**Example 3:**
```
Input:
[
  "z",
  "x",
  "z"
]

Output: ""
```

Explanation: The order is invalid, so return `""`.

**Note:**
- You may assume all letters are in lowercase.
- You may assume that if a is a prefix of b, then a must appear before b in the given dictionary.
- If the order is invalid, return an empty string.
- There may be multiple valid order of letters, return any one of them is fine.

## Solution I

Use Topological Sort with DFS. DFS topo sort maintains records of visted status of each node to find the ends of each path. In the following solution. `visited = 0` means not visited yet. `1` means visiting. `2` means visited. `-1` means the node does not exist.

#### Code

```java
class Solution {
    private final int N = 26;

    public String alienOrder(String[] words) {
        boolean[][] adj = new boolean[N][N];
        int[] visited = new int[N];
        buildGraph(words, adj, visited);

        StringBuilder sb = new StringBuilder();
        for(int i = 0; i < N; i++) {
            if(visited[i] == 0) {                 // unvisited
                if(!dfs(adj, visited, sb, i)) return "";
            }
        }
        return sb.reverse().toString();
    }

    public boolean dfs(boolean[][] adj, int[] visited, StringBuilder sb, int i) {
        visited[i] = 1;                            // 1 = visiting
        for(int j = 0; j < N; j++) {
            if(adj[i][j]) {                        // connected
                if(visited[j] == 1) return false;  // 1 => 1, cycle
                if(visited[j] == 0) {              // 0 = unvisited
                    if(!dfs(adj, visited, sb, j)) return false;
                }
            }
        }
        visited[i] = 2;                           // 2 = visited
        sb.append((char) (i + 'a'));
        return true;
    }

    public void buildGraph(String[] words, boolean[][] adj, int[] visited) {
        Arrays.fill(visited, -1);                 // -1 = not even existed
        for(int i = 0; i < words.length; i++) {
            for(char c : words[i].toCharArray()) visited[c - 'a'] = 0;
            if(i > 0) {
                String w1 = words[i - 1], w2 = words[i];
                int len = Math.min(w1.length(), w2.length());
                for(int j = 0; j < len; j++) {
                    char c1 = w1.charAt(j), c2 = w2.charAt(j);
                    if(c1 != c2) {
                        adj[c1 - 'a'][c2 - 'a'] = true;
                        break;
                    }
                }
            }
        }
    }
}
```

## Solution II

Use Topological Sort with BFS. BFS topo sort maintains the records of indegree of each node in the graph. Nodes with 0 indegree always come first.

#### Code

```java
class Solution {
    class Node {
        char c;
        Map<Character, Node> adjs;
        int indegree;

        Node(char c) {
            this.c = c;
            adjs = new HashMap();
            indegree = 0;
        }
    }

    public String alienOrder(String[] words) {
        Map<Character, Node> nodes = buildGraph(words);
        Queue<Node> q = initQueue(nodes);
        String result = buildDict(q);
        return result.length() == nodes.keySet().size()? result : "";
    }

    private String buildDict(Queue<Node> q) {
        StringBuilder sb = new StringBuilder();
        while(!q.isEmpty()) {
            Node n = q.poll();
            sb.append(n.c);
            for(Node adj : n.adjs.values()) {
                adj.indegree--;
                if(adj.indegree==0) {
                    q.offer(adj);
                }
            }
        }

        return sb.toString();
    }

    private Queue<Node> initQueue(Map<Character, Node> nodes) {
        Queue<Node> q = new LinkedList();
        for(Node n : nodes.values()) {
            if(n.indegree == 0) {
                q.offer(n);
            }
        }

        return q;
    }

    public Map<Character, Node> buildGraph(String[] words) {
        Map<Character, Node> nodes = new HashMap();
        for(int i=0; i<words.length; i++) {
            for(int j=0; j<words[i].length(); j++) {
                char c = words[i].charAt(j);
                if(!nodes.containsKey(c)) {
                    nodes.put(c, new Node(c));
                }
            }

            if(i<=0) continue;

            int len = Math.min(words[i].length(), words[i-1].length());
            for(int j=0; j<len; j++) {
                Node n1 = nodes.get(words[i-1].charAt(j));
                Node n2 = nodes.get(words[i].charAt(j));
                if(n1.c != n2.c) {
                    if(!n1.adjs.containsKey(n2.c)) {
                        n1.adjs.put(n2.c, n2);
                        n2.indegree++;
                    }
                    break;
                }
            }
        }
        return nodes;
    }
}
```

## Performance

Both O(n+edges)
