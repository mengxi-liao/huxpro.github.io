---
layout:     post
title:      "Problem: Brick Wall"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Hash Table
    - Medium
    - Array
---

## Question

There is a brick wall in front of you. The wall is rectangular and has several rows of bricks. The bricks have the same height but different width. You want to draw a vertical line from the top to the bottom and cross the least bricks.

The brick wall is represented by a list of rows. Each row is a list of integers representing the width of each brick in this row from left to right.

If your line go through the edge of a brick, then the brick is not considered as crossed. You need to find out how to draw the line to cross the least bricks and return the number of crossed bricks.

You cannot draw a line just along one of the two vertical edges of the wall, in which case the line will obviously cross no bricks.

**Example:**
```
Input: [[1,2,2,1],
        [3,1,2],
        [1,3,2],
        [2,4],
        [3,1,2],
        [1,3,1,1]]

Output: 2
```

#### Code
```java
class Solution {
    public int leastBricks(List<List<Integer>> wall) {
        Map<Integer, Integer> counter = new HashMap<>();
        int max = 0;
        for(int i=0; i<wall.size(); i++) {
            int prefixSum = 0;
            for(int j=0; j<wall.get(i).size()-1; j++) {
                prefixSum += wall.get(i).get(j);
                int count = counter.getOrDefault(prefixSum, 0) + 1;
                counter.put(prefixSum, count);
                if(count > max) max = count;
            }
        }

        return wall.size() - max;
    }
}
```

## Performance
O(n)
