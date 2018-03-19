---
layout:     post
title:      "Problem: Serialize and Deserialize Binary Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
---

## Question

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

## Solution

#### Build the Code

To build the code of a tree, we could use pre-order traversal to traverse each node of the tree and join all the nodes by a `SPLITTER` of `,`. When we reach `null`, we could mark it as an `END` with `'X'`.

For example, the following tree will have a result of `1,2,X,X,3,4,X,X,5,X,X`

```
    1
   / \
  2   3
     / \
    4   5
```

#### Build the Tree from the Code

To restore a tree, we traverse each node in the code. The first node will always be the root of the tree we are building. Then the following is the code for the left subtree followed by the code of the right subtree.

```
For 1,2,X,X,3,4,X,X,5,X,X
1 will be the root
2,X,X is the code for the left subtree
3,4,X,X,5,X,X is the code for the right subtree.
```

For the code of the left subtree and right subtree, we could use recursion to restore them.

Here is an example for the solution:

```
For 1,2,X,X,3,4,X,X,5,X,X

Traverse each node in the input from start to end:

build tree root of 1
  build a left subtree root of 2
    build a left subtree root of X, return null
    build a right subtree root of X, return null
  build a right subtree root of 3
    build a left subtree root of 4
      build a left subtree root of X, return null
      build a right subtree root of X, return null
    build a right subtree root of 5
      build a left subtree root of X, return null
      build a right subtree root of X, return null
```

#### Code

Here is a sample solution.

```java
public class Codec {
    
    private String SPLITTER = ",";
    private String END = "X";
    
    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        buildString(root, sb);
        return sb.toString();
    }
    
    public void buildString(TreeNode node, StringBuilder sb) {
        if(node == null) sb.append(END).append(SPLITTER);
        else {
            sb.append(node.val).append(SPLITER);
            buildString(node.left, sb);
            buildString(node.right, sb);
        }
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        Queue<String> q = new LinkedList();
        q.addAll(Arrays.asList(data.split(SPLITTER)));
        return deserialize(q);
    }
    
    public TreeNode deserialize(Queue<String> data) {
        String val = data.poll();
        if(val.equals(END)) return null;
        TreeNode root = new TreeNode(Integer.valueOf(val));
        root.left = deserialize(data);
        root.right = deserialize(data);
        
        return root;
    }
}
```

## Performance

Both serialize and deserialize methods traverse over each node in the tree once. So the time complexity is `O(n)`, and the space complexity is `O(n)` for using recursion and the queue.
