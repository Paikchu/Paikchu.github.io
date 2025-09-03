---
layout: post
title: "Valid Parentheses"
date: 2025-10-24
categories: leetcode
tags: [leetcode, algorithm]
---
# Valid Parentheses

Data Structure: Stack
Difficulty: Easy
Last Review Time: September 5, 2022 1:55 PM
No: 20

核心是括号配对，题比较简单，eg. [(])这样不算是正确的配对。

因此使用栈结构，进来一个开始符号时eg.(,{,[，直接放入栈中。

当准备进来一个关闭括号的符号时eg. ),},]，查找栈顶是否为对应符号，不为对应符号，则为错误匹配，正确则检查下一个字符。对应则进行pop，最后检查栈是否为空，为空为成功匹配，不为空为错误。

```cpp
class Solution {
public:
    bool isValid(string s) {
        stack<char> st;
        for(int i = 0; i < s.size(); ++i){
            if(st.empty()){
                st.push(s[i]);
            }
            else if(s[i] == ')')
            {
                if(st.top() == '(')
                    st.pop();
                else{
                    return false;
                }
            }
            else if(s[i] == '}')
            {
                if(st.top() == '{')
                    st.pop();
                else{
                    return false;
                }
            }
            else if(s[i] == ']')
            {
                if(st.top() == '[')
                    st.pop();
                else{
                    return false;
                }
            }
            else{
                st.push(s[i]);
            }
            
        }
        if(st.empty())
            return true;
        return false;
    }
};
```
