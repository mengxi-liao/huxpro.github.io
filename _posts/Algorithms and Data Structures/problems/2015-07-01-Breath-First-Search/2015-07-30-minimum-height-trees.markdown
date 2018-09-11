---
layout:     post
title:      "Problem: Minimum Height Trees"
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

For a undirected graph with tree characteristics, we can choose any node as the root. The result graph is then a rooted tree. Among all possible rooted trees, those with minimum height are called minimum height trees (MHTs). Given such a graph, write a function to find all the MHTs and return a list of their root labels.

**Format**

The graph contains n nodes which are labeled from 0 to n - 1. You will be given the number n and a list of undirected edges (each edge is a pair of labels).

You can assume that no duplicate edges will appear in edges. Since all edges are undirected, [0, 1] is the same as [1, 0] and thus will not appear together in edges.

**Example 1:**
```
Input: n = 4, edges = [[1, 0], [1, 2], [1, 3]]

        0
        |
        1
       / \
      2   3 

Output: [1]
```
**Example 2 :**
```
Input: n = 6, edges = [[0, 3], [1, 3], [2, 3], [4, 3], [5, 4]]

     0  1  2
      \ | /
        3
        |
        4
        |
        5 

Output: [3, 4]
```
**Note:**
- According to the definition of tree on Wikipedia: “a tree is an undirected graph in which any two vertices are connected by exactly one path. In other words, any connected graph without simple cycles is a tree.”
- The height of a rooted tree is the number of edges on the longest downward path between the root and a leaf.

## Solution

It is easy to see that the root of an MHT has to be the middle point (or two middle points) of the longest path of the tree.
Though multiple longest paths can appear in an unrooted tree, they must share the same middle point(s).

Computing the longest path of a unrooted tree can be done, in O(n) time, by tree dp, or simply 2 tree traversals (dfs or bfs).
The following is some thought of the latter.

Randomly select a node x as the root, do a dfs/bfs to find the node y that has the longest distance from x.
Then y must be one of the endpoints on some longest path.
Let y the new root, and do another dfs/bfs. Find the node z that has the longest distance from y.

Now, the path from y to z is the longest one, and thus its middle point(s) is the answer.

#### Code

Here is a sample solution.

```java
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {

        // Construct a graph
        List<Integer>[] children = new List[n];
        for(int i=0; i<children.length; i++) {
            children[i] = new ArrayList<Integer>();
        }
        
        for(int[] edge: edges) {
            children[edge[0]].add(edge[1]);
            children[edge[1]].add(edge[0]);
        }
        
        // use prev to record the prev node
        // of each node to trace back to construct
        // the path
        int[] prev = new int[n];
        Arrays.fill(prev, -1);
        int p0 = bfs(children, prev, 0);
        
        prev = new int[n];
        Arrays.fill(prev, -1);
        int p1 = bfs(children, prev, p0);
        
        // User prev to construct the path
        List<Integer> path = new ArrayList();
        path.add(p1);
        int i = p1;
        while(i != p0) {
            path.add(prev[i]);
            i = prev[i];
        }
        
        // Get the middle points of the path
        List<Integer> results = new ArrayList();
        results.add(path.get(path.size()/2));
        if(path.size() % 2 == 0) {
            results.add(path.get((path.size()-1)/2));
        } 
        
        return results;
    }
    
    private int bfs(List<Integer>[] children, int[] prev, int start) {
        Queue<Integer> q = new LinkedList();
        q.add(start);
        prev[start] = start;
        
        int farthest = 0;
        while(!q.isEmpty()) {
            Integer node = q.poll();
            for(int i=0; i<children[node].size(); i++) {
                int child = children[node].get(i);
                if(prev[child] == -1) {
                    prev[child] = node;
                    q.add(child);
                    farthest = child;
                }
            }
        }
        
        return farthest;
    }
}
```

## Performance

O(n)
