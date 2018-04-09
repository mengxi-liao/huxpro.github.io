---
layout:     post
title:      "Problem: Gas Station"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
---

## Question

There are *N* gas stations along a circular route, where the amount of gas at station i is `gas[i]`.

You have a car with an unlimited gas tank, and it costs `cost[i]` of gas to travel from station `i` to its next station `(i+1)`. You begin the journey with an empty tank at one of the gas stations.

Return the starting gas station's index if you can travel around the circuit once, otherwise return *-1*.

**Note:**
The solution is guaranteed to be unique.

## Solution

This problem is a little bit tricky. To solve it efficiently, we need to observe the following rules:

1. **If a car starts at A and cannot reach B. Any station between *A* and *B* can not reach *B*.(*B* is the first station that *A* cannot reach.).** That means we could randomly pick a candidate station *A* to start and see if it could reach the end. When we could not reach a station *B*, as any station between *A* and *B* could not reach *B* as well, any station between could not be a candidate.Then we could pick *B* as the new start candidate.
2. **If the total number of gas is larger than the total number of cost. There must be a solution.** That means by using the above method to loop all the stations once; we could verify the last candidate by checking if the total number of gas is larger than the total number of cost. If that's true, the candidate will be a valid start. If that's false, the circuit can not be completed.

Check the code for details.

#### Code

Here is a sample solution.

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int total = 0;
        int sum = 0;
        int start = 0;
        for(int i=0; i<gas.length; i++) {
            int fuel = gas[i] - cost[i];
            total += fuel;
            sum += fuel;
            if(sum < 0) {
                start = i+1;
                // Try starting at an earlier station,
                // since starting inside the window doesn’t help.
                // Why don't check i+1 < len? because
                // i+1 will be covered by i==0

                sum = 0;
            }
        }

        if(total < 0) return -1;
        return start;
    }
}
```

## Performance

The solution only visits each station once, so the time complexity is O(n). Only constant extra space is used.

## Proof

You may be interested in the proof of the second rule :)

**Theorem**: if the total gas is greater than the total cost, i.e., gas(1) + gas(2) + … + gas(n) > cost(1) + cost(2) + … + cost(n), there must be a way to travel around the circuit once.

**Proof**:

- If there is only one gas station, it’s true.
- If there are two gas stations a and b, and `gas(a)` cannot afford `cost(a)`, i.e., `gas(a) < cost(a)`, then `gas(b)` must be greater than `cost(b)`, i.e., `gas(b) > cost(b)`, since `gas(a) + gas(b) > cost(a) + cost(b)`; so there must be a way too.
- If there are three gas stations *a*, *b*, and *c*, where `gas(a) < cost(a)`, i.e., we cannot travel from a to b directly, then:
- Either if `gas(b) < cost(b)`, i.e., we cannot travel from *b* to *c* directly, then `cost(c) > cost(c)`, so we can start at *c* and travel to *a*; since `gas(b) < cost(b)`, `gas(c) + gas(a)` must be greater than `cost(c) + cost(a)`, so we can continue traveling from *a* to *b*. Key Point: this can be considered as there is one station at *c’* with `gas(c’) = gas(c) + gas(a)` and the cost from *c’* to b is `cost(c’) = cost(c) + cost(a)`, and the problem reduces to a problem with two stations. This in turn becomes the problem with two stations above.
- Or if `gas(b) >= cost(b)`, we can travel from *b* to *c* directly. Similar to the case above, this problem can reduce to a problem with two stations *b’* and *a*, where `gas(b’) = gas(b) + gas(c)` and `cost(b’) = cost(b) + cost(c)`. Since `gas(a) < cost(a)`, `gas(b’)` must be greater than `cost(b’)`, so it’s solved too.
- For problems with more stations, we can reduce them in a similar way. In fact, as seen above for the example of three stations, the problem of two stations can also reduce to the initial problem with one station.

