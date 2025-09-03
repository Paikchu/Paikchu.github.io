# 1823. Find the Winner of the Circular Game

Algorithm: 约瑟夫环
Data Structure: Linked List, Queue
Difficulty: Medium
Last Review Time: September 5, 2022 1:41 PM
No: 1823
Note: 递归难想的一

## 模拟+环状链表

`O(n^2), O(n^2)`

1. 构建环状链表
2. 模拟游戏过程
3. 只剩一个节点的时候返回

```cpp
struct ListC{
    int val;
    ListC* next;
    ListC() : val(0), next(nullptr) {}
    ListC(int x) : val(x), next(nullptr) {}
    ListC(int x, ListC *next) : val(x), next(next) {}
};
class Solution {
public:
    ListC* create(int i, int n){
        if(i == n){
            return nullptr;
        }
        i++;
        ListC* node = new ListC(i, create(i, n));
        return node;
    }
    int findTheWinner(int n, int k) {
        ListC* node = create(0, n);
        ListC* dummyhead = new ListC(0, node);
        while(node){
            // cout << node->val << endl;
            if(node -> next == nullptr){
                node -> next = dummyhead -> next;
                break;
            }
            node = node -> next;
        }
        cout << node -> val << endl;
        while(node -> next != node){
            for(int i = 1; i < k; ++i){
                node = node -> next;
            }
            cout << node->next-> val << endl;
            node -> next = node -> next -> next;
            // node = node -> next;
        }
        
        return node -> val;
    }
};
```

## 模拟+队列

`O(kn), O(n)`

模拟过程与上述方法类似

```cpp
class Solution {
public:
    int findTheWinner(int n, int k) {
        queue<int> q;
        for(int i = 1; i <= n; ++i){
            q.push(i);
        }
        while(q.size()!=1){
            for(int i = 1; i < k; ++i){
                q.push(q.front());
                q.pop();
            }
            q.pop();
        }
        return q.front();
    }
};
```