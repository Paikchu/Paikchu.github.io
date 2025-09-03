---
layout: post
title: "Longest Palindromic Substring"
date: 2025-10-07
categories: leetcode
tags: [leetcode, algorithm]
---
# 5. Longest Palindromic Substring

Algorithm: 双指针
Data Structure: String
Difficulty: Medium
Last Review Time: September 5, 2022 1:42 PM
No: 5

# 中心扩散

分两种情况：

1. Palindromic substring 的中心为单个字母, eg. bab, bbb
2. 中心为两个字母并排，eg. abba

```c++
class Solution {
public:
    string longestPalindrome(string s) {
        int res = 0;
        int start = 0;
        int end = 0;
        for(int i = 1; i < s.size(); ++i){
            // init state 'bb'
            if(s[i-1] == s[i]){
                int left = i-1;
                int right = i;
                int ans = 0;
                while(left >= 0 && right < s.size() && s[left] == s[right]){
                    ans+=2;
                    left--;
                    right++;
                }
                if(ans > res){
                    start = left + 1;
                    end = right - 1;
                    res = ans;
                }
            }
            // init state 'aba' or 'bbb'
            if(i + 1 < s.size() && s[i+1] == s[i-1]){
                int left = i - 1;
                int right = i + 1;
                int ans = 1;
                while(left >= 0 && right < s.size() && s[left] == s[right]){
                    ans+=2;
                    left--;
                    right++;
                }
                if(ans > res){
                    start = left + 1;
                    end = right - 1;
                    res = ans;
                }
            }
        }
        return s.substr(start, end - start + 1);
    }
};
```







```cpp
class Solution {
public:
    string longestPalindrome(string s) {
        // 中心扩散
        int ans = 0;
        int start = 0;
        int len = s.size();
        for(int p = 0; p < len; ++p){
						// 第一种情况，单个字母在中间
            int sublen = 0;
            int i;
						// 需要注意此处循环从i=1开始
            for(i = 1; p + i < len && p - i >= 0; ++i){
                if(s[p-i] == s[p+i])
                    sublen += 2;
                else
                    break;
            }
            sublen += 1;// 此处+1为字符串中心的单个字母
            if(ans < sublen){
                ans = sublen;
                start = p - i + 1;
            }
						// 第二种情况，两个字母并排
            sublen = 0;
            if(s[p+1] == s[p]){
                for(i = 0 ; p+i+1 < len && p-i >= 0; ++i){
                    if(s[p+i+1] == s[p-i])
                        sublen += 2;
                    else
                        break;
                }
                if(ans < sublen){
                    ans = sublen;
                    start = p - i + 1;
                }

            }
        }
        return s.substr(start, ans);
    }
};
```
