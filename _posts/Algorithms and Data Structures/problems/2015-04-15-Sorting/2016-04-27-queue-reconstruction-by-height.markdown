---
layout:     post
title:      "Problem: Queue Reconstruction by Height"
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
    - Medium
---

## Question

Suppose you have a random list of people standing in a queue. Each person is described by a pair of integers (h, k), where h is the height of the person and k is the number of people in front of this person who have a height greater than or equal to h. Write an algorithm to reconstruct the queue.

**Note:**
The number of people is less than 1,100.

**Example**
```
Input:
[[7,0], [4,4], [7,1], [5,0], [6,1], [5,2]]

Output:
[[5,0], [7,0], [5,2], [6,1], [4,4], [7,1]]
```

#### Solution

```
[7,0] [7,1] [6,1] [5,0] [5,2] [4,4]
```

When `[6,1]` cut in the line on the position, the `[7,1]` after that still have valid counts as he doesn't count the smaller person cut in.

翻译：矮子插队无所谓，反正高个子看不到

#### Code
```java
class Solution {
    public int[][] reconstructQueue(int[][] people) {
        Arrays.sort(people, (a, b) -> (b[0] == a[0] ? a[1] - b[1] : b[0] - a[0]));
        List<int[]> res = new ArrayList<>();
        for (int[] p : people) {
            res.add(p[1], p);
        }
        return res.toArray(new int[people.length][2]);
    }
}
```

## Performance
O(n)
