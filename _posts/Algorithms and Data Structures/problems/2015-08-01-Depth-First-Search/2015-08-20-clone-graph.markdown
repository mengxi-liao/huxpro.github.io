---
layout:     post
title:      "Problem: Clone Graph"
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

Given a reference of a node in a connected undirected graph, return a deep copy (clone) of the graph. Each node in the graph contains a val (int) and a list (List[Node]) of its neighbors.


## Solution
TODO

#### Code
```java
class Solution {
    Map<Node, Node> clonedNodes = new HashMap<>();
    public Node cloneGraph(Node node) {
        if(clonedNodes.containsKey(node)) return clonedNodes.get(node);
        Node clonedNode = new Node();
        clonedNode.val = node.val;
        clonedNode.neighbors = new ArrayList<>();
        clonedNodes.put(node, clonedNode);
        for(Node nei: node.neighbors) {
            clonedNode.neighbors.add(cloneGraph(nei));
        }
        return clonedNode;
    }
}
```

## Performance
TODO
