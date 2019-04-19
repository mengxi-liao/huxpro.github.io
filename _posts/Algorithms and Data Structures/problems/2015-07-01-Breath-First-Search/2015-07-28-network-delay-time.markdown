---
layout:     post
title:      "Problem: Network Delay Time"
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
    - Djikstra
---

## Question

There are N network nodes, labelled 1 to N.

Given times, a list of travel times as directed edges times[i] = (u, v, w), where u is the source node, v is the target node, and w is the time it takes for a signal to travel from source to target.

Now, we send a signal from a certain node K. How long will it take for all nodes to receive the signal? If it is impossible, return -1.

## Solution I

Use Djikstra

#### Code
```java
class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        PriorityQueue<int[]> pq = new PriorityQueue<int[]>((n1, n2) -> n1[1] - n2[1]);

        Map<Integer, Map<Integer, Integer>> graph = new HashMap<>();
        Map<Integer, Integer> dist = new HashMap<>();
        for(int[] e: times) {
            if(!graph.containsKey(e[0])) {
                graph.put(e[0], new HashMap<Integer, Integer>());
            }
            graph.get(e[0]).put(e[1], e[2]);
        }

        pq.add(new int[]{K, 0});
        while(!pq.isEmpty()) {
            int[] n = pq.poll();
            if(dist.containsKey(n[0])) continue;
            dist.put(n[0], n[1]);
            Map<Integer, Integer> adjs = graph.get(n[0]);
            if(adjs != null) {
                for(int adj: adjs.keySet()) {
                    int d = n[1]+adjs.get(adj);
                    if(dist.containsKey(adj)) continue;
                    pq.add(new int[]{adj, d});
                }
            }
        }

        if(dist.size() != N) return -1;
        int max = 0;
        for(int k: dist.keySet()) {
            int v = dist.get(k);
            if(v > max) max = v;
        }

        return max;
    }
}
```

## Performance
- Time Complexity: O(ElogE) in the heap implementation, as potentially every edge gets added to the heap.

- Space Complexity: O(N + E).

## Solution II

Use Bellman Ford

#### Code

class Solution {
    public int networkDelayTime(int[][] times, int N, int K) {
        int[] dist = new int[N+1];
        Arrays.fill(dist, Integer.MAX_VALUE);
        dist[K] = 0;
        for(int i=0; i<N; i++) {
            for(int[] e:times) {
                if (dist[e[0]] != Integer.MAX_VALUE && dist[e[1]] > dist[e[0]] + e[2]) {
                    dist[e[1]] = dist[e[0]] + e[2];
                }
            }
        }
        int max = 0;
        for(int i=1; i<dist.length; i++) {
            if(dist[i] > max) max = dist[i];
        }
        return max == Integer.MAX_VALUE ? -1 : max;
    }
}
