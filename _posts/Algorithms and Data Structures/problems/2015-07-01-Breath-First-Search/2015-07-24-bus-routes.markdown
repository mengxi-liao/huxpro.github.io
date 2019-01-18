---
layout:     post
title:      "Problem: Bus Routes"
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
    - Medium
---

## Question

We have a list of bus routes. Each routes[i] is a bus route that the i-th bus repeats forever. For example if routes[0] = [1, 5, 7], this means that the first bus (0-th indexed) travels in the sequence 1->5->7->1->5->7->1->... forever.

We start at bus stop S (initially not on a bus), and we want to go to bus stop T. Travelling by buses only, what is the least number of buses we must take to reach our destination? Return -1 if it is not possible.

```
Example:
Input: 
routes = [[1, 2, 7], [3, 6, 7]]
S = 1
T = 6
Output: 2
Explanation: 
The best strategy is take the first bus to the bus stop 7, then take the second bus to the bus stop 6.
```

## Solution

Use BFS

#### Code
```
class Solution {
    public int numBusesToDestination(int[][] routes, int S, int T) {
        if(S == T) return 0;
        Map<Integer, Set<Integer>> stopBusMap = new HashMap<>();
        Set<Integer>[] busStopsMap = new Set[routes.length];
        for(int bus=0; bus<routes.length; bus++) {
            busStopsMap[bus] = new HashSet<Integer>();
            for(int stop: routes[bus]) {
                busStopsMap[bus].add(stop);
                if(!stopBusMap.containsKey(stop)) stopBusMap.put(stop, new HashSet<Integer>());
                stopBusMap.get(stop).add(bus);
            }
        }
        
        Set<Integer> visited = new HashSet<Integer>();
        
        Queue<Integer> q = new LinkedList<>();
        for(int bus: stopBusMap.getOrDefault(S, new HashSet<Integer>())) {
            if(busStopsMap[bus].contains(T)) return 1;
            q.offer(bus);
            visited.add(bus);
        }
        
        int count = 1;
        while(!q.isEmpty()) {
            int size = q.size();
            for(int i=0; i<size; i++) {
                int bus = q.poll();
                Set<Integer> stopsOfBus = busStopsMap[bus];
                for(int stop: stopsOfBus) {
                    for(int adjBus: stopBusMap.get(stop)) {
                        if(busStopsMap[adjBus].contains(T)) return count+1;
                        if(visited.contains(adjBus)) continue;
                        visited.add(adjBus);
                        q.add(adjBus);
                    }
                }
            }
            count++;
        }
        
        return -1;
    }
}
```

## Performance

TODO
