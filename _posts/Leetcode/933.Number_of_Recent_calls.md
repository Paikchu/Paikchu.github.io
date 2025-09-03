# 933. Number of Recent calls

Algorithm: 模拟
Data Structure: Queue
Difficulty: Easy
Last Review Time: September 5, 2022 1:42 PM
No: 933

## 队列

将超时的请求移除

```cpp
class RecentCounter {
public:
    RecentCounter() {}
    
    int ping(int t) {
        q.push(t);
        while(q.front() < (t-3000)){
            q.pop();
        }
        return q.size();
    }
private:
    queue<int> q;
};

/**
 * Your RecentCounter object will be instantiated and called as such:
 * RecentCounter* obj = new RecentCounter();
 * int param_1 = obj->ping(t);
 */
```