---
layout:     post
title:      "Problem: Binary Tree Iterative Preorder Traversal"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Tree
    - Medium
---

## Question

Given a binary tree, return the preorder traversal of its nodes' values.

**For example:**
Given binary tree `[1,null,2,3]`,

```
   1
    \
     2
    /
   3
```

return `[1,2,3]`.

Note: Recursive solution is trivial, could you do it iteratively?


## Solution

Using a stack to simulate recursion.

- Print and push all left nodes into the stack till it hits `null`.
- Then Pop the top element from the stack, and make the `current` point to its right.
- Keep iterating until both the stack is empty and `current` is `null`.

Here is an example:

```
   1
  / \
 0   2
    /
   3

For the above tree:

stack:[]     current: 1     go_left   push  result: [1]
stack:[1]    current: 0     go_left   push  result: [1,0]
stack:[1,0]  current: null  go_right  pop
stack:[1]    current: null  go_right  pop
stack:[]     current: 2     go_left   push  result:[1,0,2]
stack:[2]    current: 3     go_left   push  result:[1,0,2,3]
stack:[2,3]  current: null  go_right  pop
stack:[2]    current: null  go_right  pop
stack:[]     current: null  return
```

#### Code

Here is a sample solution.

```java
public List<Integer> preorderTraversal(TreeNode root) {
    List<Integer> result = new ArrayList<>();
    Deque<TreeNode> stack = new ArrayDeque<>();
    TreeNode p = root;
    while(!stack.isEmpty() || p != null) {
        if(p != null) {
            stack.push(p);
            result.add(p.val);  // Add before going to children
            p = p.left;
        } else {
            TreeNode node = stack.pop();
            p = node.right;   
        }
    }
    return result;
}
```

## Performance

All the nodes in the tree are visited once. And the stack will at most store all the nodes. So both the time complexity and space complexity are both `O(n)`.
