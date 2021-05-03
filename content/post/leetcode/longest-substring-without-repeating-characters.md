---
title: "Longest Substring Without Repeating Characters"
date: 2021-05-04T01:29:14+09:00
---

## problem
[https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/)
```
Given a string s, find the length of the longest substring without repeating characters.

test case
""
"a"
"aaa"
"aaab"
"pwwkew"
"abcabcbb"

0
1
1
2
3
3
```

## o(n) approach
- 서브스트링을 관리하는 커서가 왼쪽, 오른쪽 두 개 있다.
- 커서 사이의 유니크한 문자들을 관리하는 셋이 있다
- 오른쪽 커서가 움직이면서, 유니크한 문자라면 셋이 증가하고, 유니크하지 않은 문자라면, 유니크해질때까지 왼쪽 커서를 움직인다.
- 따라서 왼쪽커서와 오른쪽커서의 사이에 있는 문자는 유니크한 문자를 가진 서브스트링임을 유지한다

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        if (s == null || s.length() == 0) {
            return 0;
        }
        
        Set<String> exists = new HashSet<String>();
        
        exists.add(s.substring(0, 1));
        
        int i = 0;
        int j = 1;
        int maxLength = 1;
        
        while (j < s.length()) {
            String right = s.substring(j, j+1);
            if (exists.contains(right)) {
                while (!exists.isEmpty() && exists.contains(right)) {
                    exists.remove(s.substring(i, i+1));
                    i++;
                }
                
            } else {
                maxLength = Math.max(maxLength, j + 1 - i);
            }
            
            exists.add(right);
            j++;
        }
        
        return maxLength;
    }
}
```