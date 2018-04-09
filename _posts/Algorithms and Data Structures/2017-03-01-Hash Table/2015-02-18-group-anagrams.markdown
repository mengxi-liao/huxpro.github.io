---
layout:     post
title:      "Problem: Group Anagrams"
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
---

## Question

Given an array of strings, group anagrams together.

For example, given: `["eat", "tea", "tan", "ate", "nat", "bat"]`,
Return:
```
[
  ["ate", "eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```

## Solution
TODO

#### Code
```java
class Solution {
    public List<List<String>> groupAnagrams(String[] strs) {
        Map<String, List<String>> map = new HashMap();
        List<List<String>> results = new ArrayList();
        for(int i=0; i<strs.length; i++) {
            String key = getSortedString(strs[i]);
            if(!map.containsKey(key)) {
                List newList = new ArrayList<String>();
                results.add(newList);
                map.put(key, newList);
            }
            map.get(key).add(strs[i]);
        }
        
        return results;
    }
    
    public String getSortedString(String s) {
        char[] ar = s.toCharArray();
        Arrays.sort(ar);
        return String.valueOf(ar);
    }
}
```

## Performance
TODO