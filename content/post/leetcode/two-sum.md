---
title: "Two Sum"
date: 2021-04-29T18:58:48+09:00
draft: true
---

## problem
[https://leetcode.com/problems/two-sum](https://leetcode.com/problems/two-sum)
```
Given an array of integers nums and an integer target, return indices of the two numbers such that they add up to target.
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
Output: Because nums[0] + nums[1] == 9, we return [0, 1].

test case
[2,5,5,11]
10
[1,2]

[2,5,5,11]
13
[0,3]
```

## o(n^2) approach
```java

```

## first approach
- two loop
- array 를 탐색하면서, value 와 value 의 index 를 hashmap 으로 저장한다
- array 를 다시 한번 탐색하면서 target - value 의 값이 haspmap 에 존재하는지, 존재한다면 index 가 현재 index 가 아닌지, 아니라면 답

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer /* value */, ArrayList<Integer> /* indices */> map = new HashMap<>();
        int len = nums.length;
        for (int i = 0; i< len; i++) {
            int val = nums[i];
            ArrayList<Integer> indices = map.get(val);
            if (indices == null) {
                ArrayList<Integer> arr = new ArrayList();
                arr.add(i);
                map.put(val, arr);
            } else {
                ArrayList<Integer> arr = map.get(val);
                arr.add(i);
                map.put(val, arr);
            }
        }
        
        for (int i = 0; i+1 < len; i++) {
            int val = nums[i];
            int valInArr = target - val;
            
            ArrayList<Integer> arr = map.get(valInArr);
            if (arr == null) {
                continue;
            }
            for (Integer j : arr) {
                if (j != i) {
                    return new int[]{i, j};
                } else {
                    continue;
                }
            }
        }
        
        return new int[]{-1, -1};
    }
}
```

## second approach
- one loop
- array 를 탐색하면서 map 에 value 와 해당 index 를 저장한다
- array 의 후반부를 탐색할 때 앞서 탐색한 value 들이 이미 map 에 저장되어 있으므로 one loop 으로 해결 가능

```java
class Solution {
    public int[] twoSum(int[] nums, int target) {
        Map<Integer /* value */, Integer /* index */> map = new HashMap<>();
        int len = nums.length;
        for (int i = 0; i< len; i++) {
            int val = nums[i];
            int valInArr = target - val;
            Integer idx = map.get(valInArr);
            if (idx == null) {
                map.put(val, i);
                continue;
            } else {
                return new int[] {idx, i};
            }
        }
        
        return new int[]{-1, -1};
    }
}
```