# 942. DI String Match

Algorithm: 贪心
Data Structure: Array
Difficulty: Easy
Last Review Time: September 5, 2022 1:42 PM
No: 942
Note: 贪心没怎么玩明白=

## 贪心

贪心思想

1. 最优子结构：规模较大的问题的解由较小的子问题构成，规模较大的解只由其中一个较小问题的解决定
2. 无后效性：后面阶段的求解不会影响前面阶段已经得到的结果
3. 贪心选择性质：从局部最优解可以得到全局最优解

对于本题：

遇到`I` 则选择当前剩余可用数字中的最小值，遇到 `D` 选择最大值。

最后 `d == i` 因为 `d = s.size()`

所以最后的代码可以改为 `ans.push_back(i)`

```cpp
class Solution {
public:
    vector<int> diStringMatch(string s) {
        vector<int> ans;
        int d = s.size();
        int i = 0;
        for(int j = 0 ; j < s.size(); ++j){
            if(s[j] == 'D'){
                ans.push_back(d);
                d--;
            }
            else {
                ans.push_back(i);
                i++;
            }
        }
        if(s[s.size()-1] == 'D'){
            ans.push_back(d);
        }
        else{
            ans.push_back(i);
        }
        
        
        return ans;
    }
};
```