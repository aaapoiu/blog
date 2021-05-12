---
title: "Reverse Bits"
date: 2021-05-12T19:15:14+09:00
---

## problem
[https://leetcode.com/problems/reverse-bits/](https://leetcode.com/problems/reverse-bits/)


## first approach
```java
public class Solution {
    // you need treat n as an unsigned value
    public int reverseBits(int n) {
        int result = 0;
        int one = 1; // 00...001
        for (int i = 0; i < 32; i++) {
            int bit = (n >> i) & one;
            result = result | (bit << (32-1-i));
        }
        
        return result;
    }
}
```