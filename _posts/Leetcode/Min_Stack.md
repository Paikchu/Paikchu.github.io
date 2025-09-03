# Min Stack

Algorithm: 构造
Data Structure: Stack
Difficulty: Medium
Last Review Time: September 5, 2022 1:47 PM
No: 155

使用vector数组作为基础数据结构，使用map来记录当前的最小值（因为其使用红黑树的结构）。使用s来记录当前的，有效元素的大小，这样就不需要删除已经pop出的元素。

```cpp
class MinStack {
public:
    int s;
    int max_size;
    vector<int> ans;
    map<int, int> min;
    MinStack() {
        ++min[INT_MAX];
        s = -1;
        max_size = -1;
    }
    void push(int val) {
        ++s;
        if(s > max_size){
            ans.push_back(val);
            max_size = s;
        }
        else{
            ans[s] = val;
        }
        ++min[val];
    }
    
    void pop() {
        --min[ans[s]];
        //cout << ans[s] <<" " << min[ans[s]] << endl;
        if(min[ans[s]] == 0){
            min.erase(ans[s]);
        }
        --s;
    }
    
    int top() {
        return ans[s];
    }
    
    int getMin() {
        return min.begin()->first;
    }
};

/**
 * Your MinStack object will be instantiated and called as such:
 * MinStack* obj = new MinStack();
 * obj->push(val);
 * obj->pop();
 * int param_3 = obj->top();
 * int param_4 = obj->getMin();
 */
```