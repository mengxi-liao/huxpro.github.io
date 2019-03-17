---
layout:     post
title:      "Problem: Maximum Frequency Stack"
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

Implement FreqStack, a class which simulates the operation of a stack-like data structure.

FreqStack has two functions:

- push(int x), which pushes an integer x onto the stack.
- pop(), which removes and returns the most frequent element in the stack.
- If there is a tie for most frequent element, the element closest to the top of the stack is removed and returned

## Solution
TODO

#### Code
```java
class FreqStack {
    int maxFreq = 0;
    Map<Integer, Stack<Integer>> freqStackMap;
    Map<Integer, Integer> valueFreqMap;

    public FreqStack() {
        valueFreqMap = new HashMap<>();
        freqStackMap = new HashMap<>();
    }

    public void push(int x) {
        int freq = valueFreqMap.getOrDefault(x, 0)+1;
        valueFreqMap.put(x, freq);
        if(freq > maxFreq) maxFreq = freq;
        Stack<Integer> stack;
        if(!freqStackMap.containsKey(freq)) {
            stack = new Stack<>();
            freqStackMap.put(freq, stack);
        }
        else {
            stack = freqStackMap.get(freq);
        }

        stack.push(x);
    }

    public int pop() {
        Stack<Integer> stack = freqStackMap.get(maxFreq);
        int x = stack.pop();
        int freq = valueFreqMap.get(x);
        if(freq == 1) valueFreqMap.remove(x);
        else valueFreqMap.put(x, freq-1);

        if(stack.isEmpty()) maxFreq--;

        return x;
    }
}

/**
 * Your FreqStack object will be instantiated and called as such:
 * FreqStack obj = new FreqStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 */
```

## Performance
O(1) for both push and pop.
