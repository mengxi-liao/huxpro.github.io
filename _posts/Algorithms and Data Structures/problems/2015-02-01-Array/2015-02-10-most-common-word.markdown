---
layout:     post
title:      "Problem: Most Common Word"
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
    - String
    - Medium
---

## Question

Given a paragraph and a list of banned words, return the most frequent word that is not in the list of banned words.  It is guaranteed there is at least one word that isn't banned, and that the answer is unique.

Words in the list of banned words are given in lowercase, and free of punctuation.  Words in the paragraph are not case sensitive.  The answer is in lowercase.

**Example:**
```
Input:
paragraph = "Bob hit a ball, the hit BALL flew far after it was hit."
banned = ["hit"]
Output: "ball"
```

**Explanation:**

`"hit"` occurs 3 times, but it is a banned word.

`"ball"` occurs twice (and no other word does), so it is the most frequent non-banned word in the paragraph.

Note that words in the paragraph are not case sensitive, that punctuation is ignored (even if adjacent to words, such as `"ball,"`), and that "hit" isn't the answer even though it occurs more because it


#### Code

Traverse the chars in the paragraph.

```java
class Solution {
    public String mostCommonWord(String paragraph, String[] banned) {
        Set<String> bannedSet = new HashSet();
        Map<String, Integer> counts = new HashMap();
        String result = null;
        int max = 0;
        for(String bannedWord : banned) {
            bannedSet.add(bannedWord);
        }

        for(int i=0; i<paragraph.length(); i++) {
            char c = paragraph.charAt(i);
            if(!valid(c))  continue;

            int begin=i;
            while(i<paragraph.length() && valid(paragraph.charAt(i))) i++;

            String w = paragraph.substring(begin, i).toLowerCase();

            if(bannedSet.contains(w)) continue;

            counts.put(w,counts.getOrDefault(w, 0)+1);

            int count = counts.get(w);
            if(count > max) {
                max = count;
                result = w;
            }
        }

        return result;
    }

    private boolean valid(char c) {
        return (c <= 'z' && c >= 'a') || (c <= 'Z' && c >= 'A');
    }
}
```

Use regular expression matching.

```java
class Solution {
    public String mostCommonWord(String p, String[] banned) {
        Set<String> ban = new HashSet<>(Arrays.asList(banned));
        Map<String, Integer> count = new HashMap<>();
        String[] words = p.toLowerCase().split("\\W+");
        for (String w : words) if (!ban.contains(w)) count.put(w, count.getOrDefault(w, 0) + 1);
        return Collections.max(count.entrySet(), Map.Entry.comparingByValue()).getKey();
    }
}
```

