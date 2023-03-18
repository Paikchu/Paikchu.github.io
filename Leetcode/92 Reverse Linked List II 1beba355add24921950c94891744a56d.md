# 92. Reverse Linked List II

Algorithm: Recursion
Data Structure: Linked List
Difficulty: Medium
Last Review Time: September 5, 2022 1:42 PM
No: 92
Note: 基于 206%20Reverse%20Linked%20List%20b269cb87e7b54cebbaca57405beaebc8.md

## shit was wrote by myself

1. 设置dummyhead返回用
2. left移动到需要处理的子链表的前一位
3. 当只有一个元素需要反转→return
4. 当有两个元素需要反转→反转→return
5. 当需要反转的元素大于两个
    1. 交换子链表的第一个位置和最后一个位置
    2. 收缩范围
    3. 重复执行a
    4. 当剩余元素只有两个时，执行第4步的反转操作

对于4，5步，right节点设置为需要交换的子链表的最后一个元素的前一个

```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode* dummyhead = new ListNode(0, head);
        ListNode* l = dummyhead;
        for(int i = 1; i < left; ++i){
            l = l -> next;
        }
        int loop = right - left;

        if (loop == 0){
            return dummyhead->next;
        }
        if(loop == 1){
            // l = l -> next;
            ListNode* r = l -> next;
            l -> next = r -> next;
            r -> next = r -> next -> next;
            l -> next -> next = r;
            
            return dummyhead->next;
        }

        for(int i = 1; i <= (right - left + 1) / 2; ++i){
            cout << "loop" << endl;
            ListNode* r = l;
            for(int j = 0 ; j < loop; ++j){
                r = r ->next;
            }
            cout << l -> val <<" " << r -> val << endl;
            ListNode* ln = l -> next;    // 2
            ListNode* lnn = l -> next -> next;   // 3
            ListNode* rnn = r -> next -> next; //5
            ListNode* rn = r -> next; // 4
            r -> next = l -> next;
            l -> next -> next = rnn;
            l -> next = rn;
            l-> next -> next = lnn;

            l = l -> next;
            loop -= 2;
            if(loop == 1){
                ListNode* r = l -> next;
                l -> next = r -> next;
                r -> next = r -> next -> next;
                l -> next -> next = r;
            
            return dummyhead->next;
        }

        }
        return dummyhead->next;
    }
};
```

## 使用206.反转链表作为子函数

reverseList函数是翻转head后的所有节点，所以需要把需要反转的链表裁切下来。

1. 找到需要翻转的最后一个元素

`for(int i = 0; i < right; ++i)
    after = after -> next;`

1. 记录这个元素后的下一个元素，方便翻转后的拼接 `ListNode* back = after ->next;`
2. 在最后一个元素后赋值为空指针，避免翻转不需要翻转的元素 `after -> next = nullptr;`

```cpp
class Solution {
public:
    ListNode* reverseList(ListNode* head) {
        if(head == nullptr){
            return head;
        }
        if(head -> next == nullptr){
            return head;
        }
        ListNode* p = reverseList(head->next);
        head -> next -> next = head;
        head -> next = nullptr;
        return p;
    }
    ListNode* reverseBetween(ListNode* head, int left, int right) {
        ListNode* dummyhead = new ListNode(0, head);
        ListNode* prev = dummyhead;
        ListNode* after = dummyhead;
        for(int i = 1; i < left; ++i){
            prev = prev -> next;
        }
        for(int i = 0; i < right; ++i){
            after = after -> next;
        }
        ListNode* back = after ->next;
        after -> next = nullptr;
        prev -> next = reverseList(prev->next);
        while(prev->next != nullptr){
            prev = prev->next;
        }
        prev -> next = back;
        return dummyhead->next;

    }
};
```