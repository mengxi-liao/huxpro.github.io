---
layout:     post
title:      "Problem: Number of Nodes in a Complete Tree"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Binary Search
    - Medium
---

## Question

Given a complete binary tree, count the number of nodes.

Definition of a complete binary tree from Wikipedia:
In a complete binary tree every level, except possibly the last, is completely filled, and all nodes in the last level are as far left as possible. It can have between 1 and 2h nodes inclusive at the last level h.

## Solution 1
TODO

#### Code
```java
class Solution {
    public int countNodes(TreeNode root) {
        TreeNode node = root;
        int count = 0;
        int level = 1;
        int leftHeight = getLeftHeight(node);
        while(node != null) {
            int l2 = getLeftHeight(node.right);
            if(leftHeight == l2+1) {
                node = node.right;
            }
            else {
                node = node.left;
            }
            count += 1 << l2;
            leftHeight --;
        }
        
        return count;
    }
    
    public int getLeftHeight(TreeNode root) {
        int h = 0;
        TreeNode node = root;
        while(node != null) {
            h++;
            node = node.left;
        }
        
        return h;
    }
}
```

#### Performance
TODO

## Solution 2
TODO

#### Code
```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        if(nums.length == 0) return new int[]{-1, -1};
        int idx = firstEleEqual(nums, target);
        int idx2 = lastEleEqual(nums, target);
        return new int[]{idx, idx2};
    }
    
    private int firstEleEqual(int[] nums, int target) {
        int l=0, r=nums.length-1;
        while(l<r) {
            int m = l + (r-l)/2;
            if(nums[m] >= target) {
                r=m;
            }
            else {
                l=m+1;   
            }
        }
        
        if(nums[r] != target) return -1;
        return r;
    }
    
    private int lastEleEqual(int[] nums, int target) {
        int l=0, r=nums.length-1;
        while(l<r) {
            int m = l + (r-l+1)/2;
            if(nums[m] <= target) {
                l=m;
            }
            else {
                r=m-1;   
            }
        }
        
        if(nums[l] != target) return -1;
        return l;
    }
}
```

#### Performance
TODO
