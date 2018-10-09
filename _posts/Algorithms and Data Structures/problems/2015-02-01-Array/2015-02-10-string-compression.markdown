---
layout:     post
title:      "Problem: String Compression"
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
    - Easy
---

## Question

Given an array of characters, compress it in-place.

The length of compression must always be smaller than or equal to the original array.

Every element of the array should be a character (not int) of length 1.

After you are done modifying the input array in-place, return the new length of the array.

**Example 1:**
```
Input:
["a","a","b","b","c","c","c"]

Output:
Return 6, and the first 6 characters of the input array should be: ["a","2","b","2","c","3"]

Explanation:
"aa" is replaced by "a2". "bb" is replaced by "b2". "ccc" is replaced by "c3".
```

**Example 2:**
```
Input:
["a"]

Output:
Return 1, and the first 1 characters of the input array should be: ["a"]

Explanation:
Nothing is replaced.
```

**Example 3:**
```
Input:
["a","b","b","b","b","b","b","b","b","b","b","b","b"]

Output:
Return 4, and the first 4 characters of the input array should be: ["a","b","1","2"].

Explanation:
Since the character "a" does not repeat, it is not compressed. "bbbbbbbbbbbb" is replaced by "b12".
Notice each digit has its entry in the array.
```

**Follow up:**
Could you solve it using only O(1) extra space?

**Note:**
1. All characters have an ASCII value in `[35, 126]`.
2. `1 <= len(chars) <= 1000`.

## Solution

1. Group the array into repeated chunks, keeping track of the character and the count. This forms the encoded contents.
2. Update the original contents with the encoded contents. We maintain an `idx` pointer to know which position to update the original array with the encoded contents and increment it according to the length of the encoded contents.

The encoded array will be shorter than the original array so that we can overwrite the original array without worries.

#### Code

Here is a sample solution.

```java
class Solution {
    public int compress(char[] chars) {
        int idx = 0;
        int i=0;
        while(i<chars.length) {
            int s = i;
            int count = 0;
            while(i<chars.length && chars[s] == chars[i]) {
                i++;
                count ++;
            }

            chars[idx++] = chars[s];
            if(count > 1) {
                char[] countChars = String.valueOf(count).toCharArray();
                for(char c : countChars) {
                    chars[idx++] = c;
                }
            }
        }

        return idx;
    }
}
```

## Performance

As each element in the array is visited once, the overall time complexity is O(n). And as it modifies the array in place, only constant extra space is used.
