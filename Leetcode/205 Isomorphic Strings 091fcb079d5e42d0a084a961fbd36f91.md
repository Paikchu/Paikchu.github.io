# 205. Isomorphic Strings

Data Structure: HashMap, String
Difficulty: Easy
Last Review Time: September 5, 2022 1:41 PM
No: 205
Note: 没有认真读题，导致第一次提交出错

# 205. 同构字符串

给定两个字符串 s 和 t ，判断它们是否是同构的。

如果 s 中的字符可以按某种映射关系替换得到 t ，那么这两个字符串是同构的。

每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。

示例 1:

```cpp
输入：s = "egg", t = "add"
输出：true

```

示例 2：

```cpp
输入：s = "foo", t = "bar"
输出：false

```

示例 3：

```cpp
输入：s = "paper", t = "title"
输出：true
```

## Analyze & Solution

### 错误分析

开始我以为题目是说，保持字符字母的连续与不连续相同就可以，如示例1和2，对于示例1，s和t的排序方式是相同的，第一个为单个字符，后两个字符连续。写出如下代码：

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        for(int i = 1; i < s.size(); ++i){
            if((s[i-1] != s[i] && t[i-1] == t[i]) || (s[i-1] == s[i] && t[i-1] != t[i])){
                return false;
            }
        }
        return true;
    }
};
```

### 正确解法

需要关注到题目中的这句话：每个出现的字符都应当映射到另一个字符，同时不改变字符的顺序。不同字符不能映射到同一个字符上，相同字符只能映射到同一个字符上，字符可以映射到自己本身。

对于案例 `s = “badc”   t = “baba”`s中的ba已经对应到了t中的ba，s中的dc不能再对应t中的ba，因为不同的字符不能对应到同一个字符上。分析到这部分，两个字符串之间是存在对应关系的，且需要快速寻找该字符是否存在对应，使用哈希表。

1. 判断当前s字符串中的当前字符是否已经出现，如果存入表中的（曾经出现的字符）的对应字符，不位当前t中的字符，则返回false
2. 如果s字符串中的当前字符没有出现过
    1. 判断t中对应的字符，是否在前面对应过其他的s字符，如果对应过则返回false
    2. 不符合条件a，则将该对应关系存入哈希表中。

```cpp
class Solution {
public:
    bool isIsomorphic(string s, string t) {
        unordered_map<char, char> map;
        for(int i = 0; i < s.size(); ++i){
            if(map.find(s[i]) != map.end()){
                if(map[s[i]] != t[i]){
                    return false;
                }
            }
            else{
                for(auto j = map.begin(); j != map.end(); ++j){
                    if(j->second == t[i])
                        return false;
                }
                map[s[i]] = t[i];
            }
        }
        return true;
    }
};
```

## 题目存在的为想到的知识点

没有认真读题