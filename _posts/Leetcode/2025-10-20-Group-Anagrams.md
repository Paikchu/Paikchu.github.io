---
layout: post
title: "Group Anagrams"
date: 2025-10-20
categories: leetcode
tags: [leetcode, algorithm]
---
# Group Anagrams

Algorithm: Sorting
Data Structure: HashMap, String
Difficulty: Medium
Last Review Time: September 5, 2022 1:51 PM
No: 49
Note: 错误思想，不应该比较acsii值，因为不同的字母可能凑出来相同的值

核心思想是要归类，具有相同字母的单词，为了能比较是否具有相同的单词，对于单词内的字符进行排序，确保具有相同字母的单词都可以正确匹配。存入map中便于快速的查找。

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> res;
        unordered_map<string, vector<string>> map;
        for(int i = 0; i < strs.size(); ++i){
            string temp = strs[i];
            string mark = temp;
            sort(mark.begin(), mark.end());
            map[mark].push_back(temp);
        }
        
        for(auto i : map){
            res.push_back(i.second);
        }
        return res;
    }
};
```
