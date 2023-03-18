# Longest Substring Without Repeating Characters

Algorithm: 滑动窗口
Data Structure: HashMap, String
Difficulty: Medium
Last Review Time: September 5, 2022 1:48 PM
No: 3

### 题目描述

给定一个字符串 `s` ，请你找出其中不含有重复字符的 **最长子串** 的长度。

**示例 1:**

```
输入: s = "abcabcbb"
输出: 3
解释: 因为无重复字符的最长子串是 "abc"，所以其长度为 3。
```

**示例 2:**

```
输入: s = "bbbbb"
输出: 1
解释: 因为无重复字符的最长子串是 "b"，所以其长度为 1。
```

**示例 3:**

```
输入: s = "pwwkew"
输出: 3
解释: 因为无重复字符的最长子串是 "wke"，所以其长度为 3。
     请注意，你的答案必须是 子串 的长度，"pwke" 是一个子序列，不是子串。
```

**示例 4:**

```
输入: s = ""
输出: 0
```

**提示：**

- `0 <= s.length <= 5 * 104`
- `s` 由英文字母、数字、符号和空格组成

### Code

`unordered_set`

```
    int lengthOfLongestSubstring(string s) {
        if(s.empty())
        {
            return 0;
        }
        unordered_set<char> ret;
        int ans = 1;
        int temp = 1;
        for(int i = 0; i < s.size(); ++i){
            ret.insert(s[i]);
            for(int j = i + 1; j < s.size(); ++j){
                if(ret.find(s[j]) != ret.end()){	// 查找是否存在相同元素
                    break;
                }
                ret.insert(s[j]);
                temp++;
            }
            ans = max(ans, temp);
            ret.clear();
            temp = 1;
        }
        return ans;
    }
```

`双指针` `滑动窗口`

```
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_set<char> windows;
        //左指针
        int l = 0;
        //右指针
        int r = 0;
        //结果
        int ans = 0;
        for(int l = 0; l < s.size(); ++l){
            if(l!=0){
                windows.erase(s[l-1]);
            }
            while(r<s.size()&&!windows.count(s[r])){
                windows.insert(s[r]);
                r++;
            }
            ans = max(ans, r - l);
        }
        return ans;
    }
};
```