---
layout:     post
title:      "Problem: Binary Tree Iterative Inorder Traversal"
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
---

## Question

Given a binary tree, return the inorder traversal of its nodes' values.

**For example:**
Given binary tree `[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return `[1,3,2]`.

Note: Recursive solution is trivial, could you do it iteratively?


## Solution

The solution will be similar to the solution for [Problem: Binary Tree Interactive Preorder Traversal](/2015/02/17/binary-tree-iterative-preorder-traversal-iterative). The only difference is instead of printing the value on pushing it to the stack, we need to print the value when the node is popped.

Here is an example:

```
   1
  / \
 0   2
    /
   3

For the above tree:

stack:[]     current: 1     go_left   push
stack:[1]    current: 0     go_left   push
stack:[1,0]  current: null  go_right  pop   result: [0]
stack:[1]    current: null  go_right  pop   result: [0,1]
stack:[]     current: 2     go_left   push
stack:[2]    current: 3     go_left   push
stack:[2,3]  current: null  go_right  pop   result: [0,1,3]
stack:[2]    current: null  go_right  pop   result: [0,1,3,2]
stack:[]     current: null  return
```

#### Code

Here is a sample solution.

```java
public List<Integer> inorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            p = p.left;
        } else {
            TreeNode node = stack.pop();
            result.add(node.val);  // Add after all left children
            p = node.right;
        }
    }
    return result;
}
```

## Performance

All the nodes in the tree are visited once. And the stack will store at most all the nodes. So both the time complexity and space complexity are both `O(n)`.
