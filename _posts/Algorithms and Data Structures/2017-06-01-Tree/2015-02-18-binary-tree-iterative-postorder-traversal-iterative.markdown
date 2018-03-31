---
layout:     post
title:      "Problem: Binary Tree Iterative Postorder Traversal"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Hard
---

## Question

Given a binary tree, return the post order traversal of its nodes' values.

**For example:**
Given binary tree `[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return `[3,2,1]`.

Note: Recursive solution is trivial, could you do it iteratively?


## Solution

The solution will be similar to the solution for [Problem: Binary Tree Interactive Preorder Traversal](/2015/02/17/binary-tree-iterative-preorder-traversal-iterative). But it's trickier.
- Instead of moving left first, we need to move right.
- Instead of adding the node to the end the result sequence, we need to prepend it to the top of the sequence.

Here is an example:

```
   1
  / \
 0   2
    /
   3

For the above tree:

stack:[]     current: 1     push  go_right    result:[1]
stack:[1]    current: 2     push  go_right    result:[2,1]
stack:[1,2]  current: null  pop   go_left
stack:[1]    current: 3     push  go_right    result:[3,2,1]
stack:[1,3]  current: null  pop   go_left
stack:[1]    current: 0     push  go_right    result:[0,3,2,1]
stack:[1,0]  current: null  pop   go_left
stack:[1]    current: null  pop   go_left
stack:[0]    current: null  return

```

#### Code

Here is a sample solution.

```java
public List<Integer> postorderTraversal(TreeNode root) {
    LinkedList<Integer> result = new LinkedList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            result.addFirst(p.val);
            p = p.right;
        } else {
            TreeNode node = stack.pop();
            p = node.left;
        }
    }
    return result;
}
```

## Performance

All the nodes in the tree are visited once. And the stack will store at most all the nodes. So both the time complexity and space complexity are both `O(n)`.
