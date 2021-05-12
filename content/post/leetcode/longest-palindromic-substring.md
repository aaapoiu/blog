---
title: "Longest Palindromic Substring"
date: 2021-05-07T16:48:22+09:00
---

## problem
[https://leetcode.com/problems/longest-palindromic-substring/](https://leetcode.com/problems/longest-palindromic-substring/)

```
Given a string s, return the longest palindromic substring in s.

"babad"
"cbbd"
"a"
"ac"

"bab"
"bb"
"a"
"a"

```

## first approach
- O(n^3)
- Time limit exceeded...

```java
class Solution {
    public String longestPalindrome(String s) {
        if (s.length() <= 1) {
            return s.substring(0, 1);
        }
        
        String longest = s.substring(0, 1);
        
        for (int i = 0; i < s.length(); i++) {
            for (int j = i+1; j <= s.length(); j++) {
                String sub = s.substring(i, j);
                if (isPalindrome(sub)) {
                    if (longest.length() < sub.length()) {
                        longest = sub;
                    } else {
                        // do nothing
                    }
                }
            }
        }
        
        return longest;
    }
    
    private boolean isPalindrome(String s) {
        for (int i = 0; i < s.length() / 2; i++) {
            Character head = s.charAt(i);
            Character tail = s.charAt(s.length()-1-i);
            if (!head.equals(tail)) {
                return false;
            }
        }
        
        return true;
    }
}
```

## second approach
- description

```java

// code

```


