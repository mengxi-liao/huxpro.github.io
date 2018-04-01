---
layout:     post
title:      "Problem: Compare Version Numbers"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Array
    - Medium
---

## Question

Compare two version numbers version1 and version2.
If version1 > version2 return 1, if version1 < version2 return -1, otherwise return 0.

You may assume that the version strings are non-empty and contain only digits and the . character.
The . character does not represent a decimal point and is used to separate number sequences.
For instance, 2.5 is not "two and a half" or "half way to version three", it is the fifth second-level revision of the second first-level revision.

Here is an example of version numbers ordering:

```
0.1 < 1.1 < 1.2 < 13.37
```

## Solution

After reading the requirements, we should notice there are several cases:
1. The two input version numbers may have different number of parts. For example, `1.2.3` and `2.3`
2. Each part of a version is just a string with digits. Converting them to `int` or `long` may cause overflow.
3. We should compare the versions part by part, from left to right. Once a part in `version1` is different from the part in `version2`, we should be able to get the result.

Here is a simple solution. Traverse the two versions at the same time. Every time we extract a part, `p1`, from `version1`, and extract a part2, `p2`, from `version2`. Then compare the two parts. If `p1==p2`, continue to compare the parts after. If `p1 > p2`, return `1`. If `p1 < p2`, return `-1`.

How to handle the case when the two versions have a different number of parts? We could define the corresponding part in the short version as 0. For example, for the case of `1.2.3 vs 1.2`,  convert `1.2` to `1.2.0`. As `3>0`, return `1`.

#### Code

First, implement the code for extracting parts.

```java
class Solution {
    public int compareVersion(String version1, String version2) {
        int i=0, j=0;
        while(i<version1.length() || j<version2.length()) {
            StringBuilder sbV1Part = new StringBuilder();
            while(i<version1.length() && version1.charAt(i) != '.') {
                sbV1Part.append(version1.charAt(i++));
            }


            StringBuilder sbV2Part = new StringBuilder();
            while(j<version2.length() && version2.charAt(j) != '.') {
                sbV2Part.append(version2.charAt(j++));
            }

            int partResult = compareParts(sbV1Part, sbV2Part);
            if(partResult != 0) return partResult;

            i++;
            j++;
        }
        return 0;
    }
}
```

Now we need to implement `compareParts`. We won't convert the parts to `int` as it may cause overflow. The trick here is to convert the two
parts to have the same length. For example, `12 vs 1234` could be converted to `0012 vs 1234`.

```java
public int compareParts(StringBuilder v1, StringBuilder v2) {
    int lenDiff = v1.length() - v2.length();
    StringBuilder leadingZeros = new StringBuilder();
    int absLenDiff = Math.abs(lenDiff);
    while(absLenDiff > 0) {
        leadingZeros.append('0');
        absLenDiff--;
    }
    if(lenDiff>0) v2 = leadingZeros.append(v2);
    else v1 = leadingZeros.append(v1);

    for(int i=0; i<v1.length(); i++) {
        if(Integer.valueOf(v1.charAt(i)) > Integer.valueOf(v2.charAt(i))) return 1;
        if(Integer.valueOf(v1.charAt(i)) < Integer.valueOf(v2.charAt(i))) return -1;
    }

    return 0;
}
```

#### Performance

Time complexity is O(n). It uses two `StringBuilder` to store the parts, so the space complexity is `O(number of digits in a part)`.
