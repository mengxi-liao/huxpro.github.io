---
layout:     post
title:      "Problem: Permutations II"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Depth First Search
    - Medium
---

## Question

Given a collection of distinct numbers, return all possible permutations.

For example,
`[1,2,3]` have the following permutations:
```
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```

**Follow up:**
What if the collection has duplicate numbers?

## Solution 1

If we are allowed to sort the array, we could sort the array to let the same number cluster together. In this way, avoiding duplicates, which is to prevent the same number being the first number in the permutation, is simplified because we can judge is a number is the same as its previous one and if its previous one has been used. We keep a boolean array to store the numbers being used, whose values are false initially. Each time we use a number, we set its corresponding value in the boolean array to be true. And we try further down in the recursion. Once the recursion returns, we backtrack by changing its corresponding boolean value to be false and remove it from the current result.

#### Code
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> results = new ArrayList();
        boolean[] used = new boolean[nums.length];
        List<Integer> collector = new ArrayList();
        
        Arrays.sort(nums);
        
        collect(nums, used, collector, results);
        
        return results;
    }
    
    public void collect(int[] nums, boolean[] used, List<Integer> collector, List<List<Integer>> results) {
        if(collector.size() == nums.length) {
            results.add(new ArrayList<Integer>(collector));
            return;
        }
        
        int prev = -1;
        for(int i=0; i<nums.length; i++) {
            if(used[i]) continue;
            if(prev >= 0 && nums[i] == nums[prev]) continue;
            used[i] = true;
            prev = i;
            collector.add(nums[i]);
            collect(nums, used, collector, results);
            collector.remove(collector.size()-1);
            used[i]  = false;
        }
    }
}
```

#### Performance

O(n!) time, O(n) space

## Solution 2

Based on the third method of permutations I, which is to swap two numbers in the array each time. However, we want to avoid duplicates in this problem. Avoiding duplicates in the permutations we got is avoiding let the same number to be the first number of the permutations. And this is also true in the subproblems we met. So we keep a HashSet at each level of the recursion tree to store the numbers we have used as the first number of the permutations generated from this level Once we find a number already existed in the HashSet, we would skip this number. Other ideas are the same as Permutations I. Swap 2 numbers each time, recurse, and swap back. A typical backtracking problem. 

#### Code
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ret = new ArrayList<>();
        if (nums == null || nums.length == 0) return ret;
        
        permuteHelper(nums, 0, ret);
        
        return ret;
    }
    
    private void permuteHelper(int[] nums, int pos, List<List<Integer>> ret) {
        if (pos == nums.length) {
            List<Integer> curr = new ArrayList<>();
            for (int num : nums) {
                curr.add(num);
            }
            ret.add(curr);
            return;
        }
        
        Set<Integer> used = new HashSet<>();
        for (int i = pos; i < nums.length; i++) {
            if (used.add(nums[i])) {
                swap(nums, pos, i);
                permuteHelper(nums, pos + 1, ret);
                swap(nums, pos, i); //Backtracking
            } 
        }
    }
    
    private void swap(int[] nums, int i, int j) {
        if (i == j) return;
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```

#### Performance

O(n!) time. O(n ^ 2) space. The recursion would be n-level in depth. 

## Solution 3

If the nums array cannot be changed (i.e., cannot sort the array), then we may need to keep something to record which number has been used. In this question, we maintain a hashmap with the numbers in the nums as the key and the number of their appearance as the value
So each time we used a number, we subtract its presence by 1 and searching down by recursion. So we only use the number with appearance greater than 0. Once we reached the length of the nums, we add current result into the ret list. And by the time the recursion returns, we backtrack by adding back 1 to the appearance and remove the last number of current result. 

#### Code
```java
class Solution {
    public List<List<Integer>> permuteUnique(int[] nums) {
        List<List<Integer>> ret = new ArrayList<>();
        if (nums == null || nums.length == 0) return ret;
        Map<Integer, Integer> used = new HashMap<Integer, Integer>();//<number, appearance>
        for (int num : nums) {
            if (used.containsKey(num)) {
                used.put(num, used.get(num) + 1);
            } else {
                used.put(num, 1);
            }
        }
        permuteHelper(nums, 0, ret, new ArrayList<Integer>(), used);
        
        return ret;
    }
    
    private void permuteHelper(int[] nums, int start, List<List<Integer>> ret, List<Integer> curr, Map<Integer, Integer> used) {
        if (start == nums.length) {
            ret.add(new ArrayList<Integer>(curr));
            return;
        }
        
        Set<Integer> keys = used.keySet();
        for (Integer key : keys) { //iterate through the hashmap to generate permutations
            if (used.get(key) > 0) {
                used.put(key, used.get(key) - 1);
                curr.add(key);
                permuteHelper(nums, start + 1, ret, curr, used);
                curr.remove(curr.size() - 1);
                used.put(key, used.get(key) + 1);
            }
        }
    }
    
}
```

#### Performance

O(n!) time, O(n) space with considering the recursion stack. The recursion stack would consume O(n) space since the recursion would be n-level in depth where n is the length of nums. 

## Credit

Credit for YaokaiYang for the solutions with detailed explanations here https://leetcode.com/problems/permutations-ii/discuss/18677/3-different-Java-solution-for-this-question-with-detailed-explanation

