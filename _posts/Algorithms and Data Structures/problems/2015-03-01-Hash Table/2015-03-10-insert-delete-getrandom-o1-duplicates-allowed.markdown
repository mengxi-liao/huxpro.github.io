---
layout:     post
title:      "Problem: Insert Delete GetRandom O(1)"
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

Design a data structure that supports all following operations in average O(1) time.

**Note: Duplicate elements are allowed.**
- insert(val): Inserts an item val to the collection.
- remove(val): Removes an item val from the collection if present.
- getRandom: Returns a random element from current collection of elements. The probability of each element being returned is linearly related to the number of same value the collection contains.


**Example:**

```
// Init an empty collection.
RandomizedCollection collection = new RandomizedCollection();

// Inserts 1 to the collection. Returns true as the collection did not contain 1.
collection.insert(1);

// Inserts another 1 to the collection. Returns false as the collection contained 1. Collection now contains [1,1].
collection.insert(1);

// Inserts 2 to the collection, returns true. Collection now contains [1,1,2].
collection.insert(2);

// getRandom should return 1 with the probability 2/3, and returns 2 with the probability 1/3.
collection.getRandom();

// Removes 1 from the collection, returns true. Collection now contains [1,2].
collection.remove(1);

// getRandom should return 1 and 2 both equally likely.
collection.getRandom();
```

## Solution
User a map to track the position of the values in the list.
Use a list to track the order of values.

#### Code
```java
class RandomizedCollection {
    Map<Integer, Set<Integer>> map = new HashMap<>();
    List<Integer> list = new ArrayList<>();
    Random rand = new Random();

    /** Initialize your data structure here. */
    public RandomizedCollection() {

    }

    public boolean insert(int val) {
        if(!map.containsKey(val)) {
            map.put(val, new HashSet<Integer>());
            map.get(val).add(list.size());
            list.add(val);
            return true;
        }
        else {
            map.get(val).add(list.size());
            list.add(val);
            return false;
        }
    }

    /** Removes a value from the collection. Returns true if the collection contained the specified element. */
    public boolean remove(int val) {
        if(!map.containsKey(val)) return false;
        Set<Integer> set = map.get(val);
        int index = set.iterator().next();
        set.remove(index);
        if(set.isEmpty()) map.remove(val);
        int lastIndex = list.size()-1;
        if(index == lastIndex) {
            list.remove(index);
        }
        else {
            int lastVal = list.get(lastIndex);
            list.set(index, lastVal);
            Set<Integer> setLastVal = map.get(lastVal);
            setLastVal.remove(lastIndex);
            setLastVal.add(index);
            list.remove(lastIndex);
        }

        return true;
    }

    /** Get a random element from the collection. */
    public int getRandom() {
        return list.get(rand.nextInt(list.size()));
    }
}

/**
 * Your RandomizedCollection object will be instantiated and called as such:
 * RandomizedCollection obj = new RandomizedCollection();
 * boolean param_1 = obj.insert(val);
 * boolean param_2 = obj.remove(val);
 * int param_3 = obj.getRandom();
 */
```

## Performance
`O(1)`
