---
layout: post
title: "Reverse Linked List"
date: 2025-09-24
categories: leetcode
tags: [leetcode, algorithm]
---
# 206. Reverse Linked List

Algorithm: Recursion
Data Structure: Linked List
Difficulty: Easy
Last Review Time: January 8, 2023 11:00 PM
No: 206
Note: 进阶 92%20Reverse%20Linked%20List%20II%201beba355add24921950c94891744a56d.md ，7.9日这题递归没写出来

[力扣](https://leetcode-cn.com/problems/reverse-linked-list/)

## 迭代

`O(n), O(1)`

1. 设置prev节点初始化为nullptr
2. 设置curr节点为head节点
3. 设置next节点标记curr的下一个节点
4. curr只想prev节点
5. prev来到curr节点
6. curr节点跳到next节点

![IMG_0585.jpg](206%20Reverse%20Linked%20List%20b269cb87e7b54cebbaca57405beaebc8/IMG_0585.jpg)

![IMG_0586.JPG](206%20Reverse%20Linked%20List%20b269cb87e7b54cebbaca57405beaebc8/IMG_0586.jpg)

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
    ListNode* reverseList(ListNode* head) {
        ListNode* curr = head;
        ListNode* prev = nullptr;
        while(curr){
            ListNode* next = curr -> next;
            curr -> next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
};
```

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
    ListNode* reverseList(ListNode* head) {
        ListNode* dummyhead = new ListNode(0, head);
        ListNode* prev = nullptr;
        ListNode* curr = head; 
        ListNode* back = curr -> next;
        while(back != nullptr){
            curr -> next = prev;
            prev = curr;
            curr = back;
            back = back -> next;
        }
        curr -> next = prev;
        return curr;
    }
};
```

## Recursion

`O(n), O(n)`

1. 关注边界条件，当链表的长度为0，`head == nullptr` 时直接`return head`
2. 递归的递：（递归语句之前的部分）
    1. 当head→next == nullptr 时终止递推，进入归的部分
    2. 把当前的head记录为p，作为反转后链表的头节点
3. 递归的归：（递归语句之后的部分）
    1. 让当前节点的下一个节点指向自己 `head → next → next == head`
    2. 因为原始列表的第一个元素，需要指向nullptr，所以我们需要让当前节点指向空，避免链表成环 `head→next = nullptr`
        
        ![Page2.jpg](206%20Reverse%20Linked%20List%20b269cb87e7b54cebbaca57405beaebc8/Page2.jpg)
        
    3. 返回新的头节点p

![Page1.jpg](206%20Reverse%20Linked%20List%20b269cb87e7b54cebbaca57405beaebc8/Page1.jpg)

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
};
```
