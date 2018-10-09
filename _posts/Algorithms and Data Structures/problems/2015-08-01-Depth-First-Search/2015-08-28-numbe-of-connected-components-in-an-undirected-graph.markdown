---
layout:     post
title:      "Problem: Number of Connected Components in an Undirected Graph"
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
    - Union Find
    - Medium
---

## Question

Given `n` nodes labeled from 0 to `n - 1` and a list of undirected edges (each edge is a pair of nodes), write a function to find the number of connected components in an undirected graph.

**Example 1:**

```
     0          3
     |          |
     1 --- 2    4
```
Given `n = 5` and `edges = [[0, 1], [1, 2], [3, 4]]`, return `2`.

[0, 1] [1,2] [2,0]
0       0    0

[0,4] [1,2] [2,1] [4,2]
 0     1     1     1 

**Example 2:**

```
     0           4
     |           |
     1 --- 2 --- 3
```
Given `n = 5` and `edges = [[0, 1], [1, 2], [2, 3], [3, 4]]`, return `1`.

**Note:**
You can assume that no duplicate edges will appear in `edges`. Since all edges are undirected, `[0, 1]` is the same as `[1, 0]` and thus will not appear together in `edges`.

## Solution 1

Use DFS.

#### Code
```java
class Solution {
    class Node {
        boolean visited = false;
        List<Node> nodes = new ArrayList();
        int label;
    }
    
    public int countComponents(int n, int[][] edges) {        
        Map<Integer, Node> nodesMap = new HashMap();
        
        for(int i=0; i<edges.length; i++) {
            int[] e = edges[i];
            Node n1 = createOrFindNode(e[0], nodesMap);
            Node n2 = createOrFindNode(e[1], nodesMap);            
            n1.nodes.add(n2);
            n2.nodes.add(n1);
        }
        
        for(Node node: nodesMap.values()) {
            if(node.visited) n--;
            else dfs(node);
        }
        
        return n;
    }
    
    private Node createOrFindNode(int label, Map<Integer, Node> nodesMap) {
        Node n = null;
        if(nodesMap.containsKey(label))
            n = nodesMap.get(label);
        else {
            n = new Node();
            n.label = label;
            nodesMap.put(label, n);
        }
        
        return n;
    }
    
    private void dfs(Node n) {
        if(n.visited) return;
        n.visited = true;
        for(Node child: n.nodes) {
            dfs(child);
        }
    }
}

```

#### Performance

Every node will be at most visited once. There are `edges.length` nodes, `e`. So the overall performance is `O(e)`.

## Solution 2

Union Find

#### Code
```java
class Solution {
    public int countComponents(int n, int[][] edges) {
        int[] roots = new int[n];
        for(int node=0; node<n; node++) {
            roots[node] = node;
        }
        
        int count = n;
        
        for(int[] e : edges) {
            int root1 = findRoot(roots, e[0]);
            int root2 = findRoot(roots, e[1]);
            if(root1 != root2) {
                count--;
                roots[root1] = root2;
            }
        }
        
        return count;
    }
    
    private int findRoot(int[] roots, int node) {
        //find the root of node
        int finder = node;
        while(roots[finder] != finder) {
            finder = roots[finder];
        }
        
        //update the roots map to cache the updated root of node
        roots[node] = finder;
        
        return finder;
    }
}

```

#### Performance
TODO
