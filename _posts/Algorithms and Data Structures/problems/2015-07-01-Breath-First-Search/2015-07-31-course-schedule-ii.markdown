---
layout:     post
title:      "Problem: Course Schedule II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Breadth First Search
    - Depth First Search
    - Hard
    - Topological Sort
---

## Question

There are a total of n courses you have to take, labeled from 0 to n-1.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: [0,1]

Given the total number of courses and a list of prerequisite pairs, return the ordering of courses you should take to finish all courses.

There may be multiple correct orders, you just need to return one of them. If it is impossible to finish all courses, return an empty array.

**Example 1:**
```
Input: 2, [[1,0]]
Output: [0,1]
Explanation: There are a total of 2 courses to take. To take course 1 you should have finished
             course 0. So the correct course order is [0,1] .
```
**Example 2:**
```
Input: 4, [[1,0],[2,0],[3,1],[3,2]]
Output: [0,1,2,3] or [0,2,1,3]
Explanation: There are a total of 4 courses to take. To take course 3 you should have finished both
             courses 1 and 2. Both courses 1 and 2 should be taken after you finished course 0.
             So one correct course order is [0,1,2,3]. Another correct ordering is [0,2,1,3] .
```

## Solution I

Use Topological Sort with DFS. DFS topo sort maintains records of visted status of each node to find the ends of each path. In the following solution. `visited = 0` means not visited yet. `1` means visiting. `2` means visited.

#### Code

```java
class Solution {
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<Integer>[] pres = new List[numCourses];
        int[] visited = new int[numCourses];

        for(int i=0; i<numCourses; i++) pres[i] = new ArrayList<>();
        for(int[] pre:prerequisites) pres[pre[0]].add(pre[1]);

        List<Integer> results = new ArrayList<>();
        for(int i=0; i<numCourses; i++) {
            if(visited[i] == 0) {
                if(!dfs(pres, i, visited, results)) return new int[]{};
            }
        }

        int[] arr = new int[results.size()];
        for(int i=0; i<results.size(); i++) {
            arr[i] = results.get(i);
        }

        return arr;
    }

    // DFS topo sort. Start from a random node, and
    // reach the root node with 0 out degree
    boolean dfs(List<Integer>[] pres, int i, int[] visited, List<Integer> results) {
        visited[i] = 1;
        for(int j: pres[i]) {
            if(visited[j] == 1) return false;
            if(visited[j] == 2) continue;
            if(!dfs(pres, j, visited, results)) return false;
        }
        if(visited[i] == 1) results.add(i);
        visited[i] = 2;

        return true;
    }
}
```

## Performance

Both O(n+edges)
