---
layout:     post
title:      "Problem: String to Integer (atoi)"
date:       2015-02-18 00:00:00
author:     "Marcy"
header-img: "img/post-bg-2015.jpg"
catalog: true
category: algnote
algnote-tags:
    - Coding Interview
    - Coding Practice
    - Algorithms and Data Structures
    - Math
    - Hard
---

## Question

Implement atoi to convert a string to an integer.

**Hint:** Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

**Notes:** It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

**Requirements for atoi:**

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned. If the correct value is out of the range of representable values, `INT_MAX (2147483647`) or `INT_MIN (-2147483648)` is returned.

## Solution
TODO

#### Code
```java
class Solution {
    public int myAtoi(String str) {
        str = str.trim();
        if(str.length() == 0) return 0;

        int carry  = 1;
        if(str.charAt(0) == '-') carry = -1;
        int idx = 0;
        if(str.charAt(0) == '-' || str.charAt(0) == '+') {
            idx++;
        }

        int result = 0;
        while(idx < str.length()) {
            char c = str.charAt(idx);
            if(c < '0' || c > '9') return result;

            int v = carry * (c - '0');
            if(result > Integer.MAX_VALUE/10 || 
               result == Integer.MAX_VALUE/10 && v > 7) return Integer.MAX_VALUE;
            if(result < Integer.MIN_VALUE/10 || 
               result == Integer.MIN_VALUE/10 && v < -8) return Integer.MIN_VALUE;
            result = result * 10 + v;
            idx++;
        }

        return result;
    }
}
```

## Performance
TODO
