---
layout: post
title: "Subarray Product Less Than K"
date: 2025-10-13
categories: leetcode
tags: [leetcode, algorithm]
---
# 713. Subarray Product Less Than K

Algorithm: 滑动窗口
Data Structure: Array
Difficulty: Medium
Last Review Time: September 5, 2022 1:42 PM
No: 713

## 滑动窗口

关键因素在于`ans += r - l - 1` 这个式子。

经过前面的两层循环，得到的这个区间内的所有数的乘积都是小于k的，而r前所有数字的子数组已经列举完毕，只需要加上已nums[r]为结尾，nums[l]为开头的所有子数组的数量。

```cpp
class Solution {
public:
    int numSubarrayProductLessThanK(vector<int>& nums, int k) {
        int l = 0;
        int r = 0;
        int m = 1;
        int ans = 0;
        for(;r < nums.size(); ++r){
            m *= nums[r];
            while(l <= r && m >= k){
                m /= nums[l];
                l++;
            }
            ans += r - l + 1; // 每次加上以当前数字为结尾的所有子数组数量
            }
        return ans;
    }
};
```
