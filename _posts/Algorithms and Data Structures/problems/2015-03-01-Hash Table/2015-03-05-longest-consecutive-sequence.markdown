---
layout:     post
title:      "Problem: Longest Consecutive Sequence"
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
    - Hard
---

## Question

Given an unsorted array of integers, find the length of the longest consecutive elements sequence.

For example,
Given `[100, 4, 200, 1, 3, 2]`,
The longest consecutive elements sequence is `[1, 2, 3, 4]`. Return its length: `4`.

Your algorithm should run in O(n) complexity.

## Solution
TODO

#### Code
```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Set<Integer> set = new HashSet<>();
        for(int n:nums) set.add(n);
        Iterator<Integer> itr = set.iterator();
        int len = 0;
        for(int val: nums) {
            if(!set.contains(val)) continue;
            int upper = val;
            while(set.contains(upper)) {
                set.remove(upper);
                upper++;
            }
            int lower = val-1;
            while(set.contains(lower)) {
                set.remove(lower);
                lower--;
            }

            len = Math.max(len, upper - lower -1);
        }
        return len;
    }
}
```

```java
class Solution {
    public int longestConsecutive(int[] nums) {
        Map<Integer, int[]> map = new HashMap();
        int max = 0;
        for(int i=0; i<nums.length; i++) {
            if(map.containsKey(nums[i])) continue;
            int[] entry = new int[] { nums[i], nums[i] };
            int[] left = entry;
            int[] right = entry;
            if(map.containsKey(nums[i]-1)) {
                left = map.get(map.get(nums[i]-1)[0]);
            }
            
            if(map.containsKey(nums[i]+1)) {
                right = map.get(map.get(nums[i]+1)[1]);
            }
            
            map.put(nums[i], entry);
            left[1] = right[1];
            right[0] = left[0];
            
            max = Math.max(max, right[1] - left[0] + 1);
        }
        
        return max;
    }
}
```

## Performance
TODO
