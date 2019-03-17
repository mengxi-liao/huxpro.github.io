---
layout:     post
title:      "Problem: Implement Queue using Stacks"
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
    - Easy
---

## Question

Implement the following operations of a queue using stacks.

- push(x) -- Push element x to the back of queue.
- pop() -- Removes the element from in front of queue.
- peek() -- Get the front element.
- empty() -- Return whether the queue is empty.

**Notes:**
- You must use only standard operations of a stack -- which means only push to top, peek/pop from top, size, and is empty operations are valid.
- Depending on your language, stack may not be supported natively. You may simulate a stack by using a list or deque (double-ended queue), as long as you use only standard operations of a stack.
- You may assume that all operations are valid (for example, no pop or peek operations will be called on an empty queue).

## Solution
TODO

#### Code
```java
class MyQueue {
    
    Stack<Integer> pushStack = new Stack();
    Stack<Integer> popStack = new Stack();
    
    /** Initialize your data structure here. */
    public MyQueue() {
        
    }
    
    /** Push element x to the back of queue. */
    public void push(int x) {
        pushStack.push(x);
    }
    
    public void preparePopStack() {
        while(!pushStack.empty()) {
            popStack.push(pushStack.pop());
        }
    }
    
    /** Removes the element from in front of queue and returns that element. */
    public int pop() {
        if(empty()) return -1;
        if(popStack.empty()) {
            preparePopStack();
        }
        
        return popStack.pop();
    }
    
    /** Get the front element. */
    public int peek() {
        if(empty()) return -1;
        if(popStack.empty()) {
            preparePopStack();
        }
        
        return popStack.peek();
    }
    
    /** Returns whether the queue is empty. */
    public boolean empty() {
        return pushStack.empty() && popStack.empty();
    }
}

```

## Performance
TODO
