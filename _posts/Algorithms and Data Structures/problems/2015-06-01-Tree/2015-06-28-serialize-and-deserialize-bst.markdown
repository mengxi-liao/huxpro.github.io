---
layout:     post
title:      "Problem: Serialize and Deserialize BST"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Binary Tree
    - Binary Search Tree
    - Medium
---

## Question

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary search tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary search tree can be serialized to a string and this string can be deserialized to the original tree structure.

**The encoded string should be as compact as possible.**

Note: Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

## Solution

TODO

#### Code

Here is a sample solution.

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Codec {

    // Encodes a tree to a single string.
    public String serialize(TreeNode root) {
        List<String> list = new ArrayList<>();
        serialize(root, list);
        return String.join(" ", list);
    }

    private void serialize(TreeNode root, List<String> list) {
        if(root == null) return;
        list.add(String.valueOf(root.val));
        serialize(root.left, list);
        serialize(root.right, list);
    }

    // Decodes your encoded data to tree.
    public TreeNode deserialize(String data) {
        if(data.length() == 0) return null;
        Queue<Integer> q = new LinkedList<>();
        String[] list = data.split(" ");
        for(String s: list) {
            q.offer(Integer.valueOf(s));
        }

        return deserialize(q, Long.MIN_VALUE, Long.MAX_VALUE);
    }

    public TreeNode deserialize(Queue<Integer> q, long min, long max) {
        if(q.isEmpty()) return null;
        if(q.peek() < min || q.peek() > max) return null;
        int val = q.poll();

        TreeNode n = new TreeNode(val);
        n.left = deserialize(q, min, val);
        n.right = deserialize(q, val, max);

        return n;
    }
}

// Your Codec object will be instantiated and called as such:
// Codec codec = new Codec();
// codec.deserialize(codec.serialize(root));
```

## Performance

Both serialize and deserialize methods traverse over each node in the tree once. So the time complexity is `O(n)`, and the space complexity is `O(n)` for using recursion and the queue.
