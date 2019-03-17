---
layout:     post
title:      "Problem: Flatten Nested List Iterator"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Stack
    - Hard
---

## Question

Given a nested list of integers, implement an iterator to flatten it.

Each element is either an integer, or a list -- whose elements may also be integers or other lists.

**Example 1:**
```
Input: [[1,1],2,[1,1]]
Output: [1,1,2,1,1]
Explanation: By calling next repeatedly until hasNext returns false, 
             the order of elements returned by next should be: [1,1,2,1,1].
```
**Example 2:**
```
Input: [1,[4,[6]]]
Output: [1,4,6]
Explanation: By calling next repeatedly until hasNext returns false, 
             the order of elements returned by next should be: [1,4,6].
```

## Solution
TODO

#### Code
```java
/**
 * // This is the interface that allows for creating nested lists.
 * // You should not implement it, or speculate about its implementation
 * public interface NestedInteger {
 *
 *     // @return true if this NestedInteger holds a single integer, rather than a nested list.
 *     public boolean isInteger();
 *
 *     // @return the single integer that this NestedInteger holds, if it holds a single integer
 *     // Return null if this NestedInteger holds a nested list
 *     public Integer getInteger();
 *
 *     // @return the nested list that this NestedInteger holds, if it holds a nested list
 *     // Return null if this NestedInteger holds a single integer
 *     public List<NestedInteger> getList();
 * }
 */
public class NestedIterator implements Iterator<Integer> {
    Stack<Iterator<NestedInteger>> s = new Stack<>();
    Integer next = null;

    public NestedIterator(List<NestedInteger> nestedList) {
        s.push(nestedList.iterator());
        computeNext();
    }

    @Override
    public Integer next() {
        int n = next;
        next = null;
        return n;
    }

    @Override
    public boolean hasNext() {
        computeNext();
        return next != null;
    }

    private void computeNext() {
        while(next == null && !s.isEmpty()) {
            Iterator<NestedInteger> itr = s.peek();
            // Allow empty list in the stack. We just clean that here.
            if(!itr.hasNext()) {
                s.pop();
                continue;
            }
            NestedInteger n = itr.next();
            if(n.isInteger()) next = n.getInteger();
            else s.push(n.getList().iterator());
        }
    }
}

/**
 * Your NestedIterator object will be instantiated and called as such:
 * NestedIterator i = new NestedIterator(nestedList);
 * while (i.hasNext()) v[f()] = i.next();
 */
```

## Performance
TODO
