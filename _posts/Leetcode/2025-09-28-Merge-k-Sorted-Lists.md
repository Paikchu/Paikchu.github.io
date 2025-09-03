---
layout: post
title: "Merge k Sorted Lists"
date: 2025-09-28
categories: leetcode
tags: [leetcode, algorithm]
---
# Merge-k-Sorted-Lists





#### Compare one by one

TC: O(kN)

SC: O(1)

Create a head node which point to the smallest(not nullptr) head node of k lists unitl head connect all the nodes in k lists.

```
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0){
            return nullptr;
        }
        int m = 1;
        ListNode* head = new ListNode(0);
        ListNode* dummyhead;
        dummyhead = head;
        while(m != -1){
            m = -1;
            int mini = INT_MAX;
            // Find minimum
            for(int i = 0; i < lists.size(); ++i){
                if(lists[i] != nullptr && lists[i]->val < mini){
                    m = i;
                    mini = lists[i]->val;
                }
            }
            if(m!=-1){
                head -> next = lists[m];
                head = head -> next;
                lists[m] = lists[m] -> next;
            }
            else{
                head->next = nullptr;
            }
        }
        return dummyhead->next;
    }
}
```



#### Optimize with priority queue

TC: O(Nlogk)

SC: O(1)

```
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
class Compare {
public:
    bool operator()(ListNode* below, ListNode* above)
    {
        if (below->val > above->val) {
            return true;
        }else{
            return false;
        }
    }
 };
class Solution {
public:
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.size() == 0){
            return nullptr;
        }
        int m = 1;
        ListNode* head = new ListNode(0);
        ListNode* dummyhead;
        dummyhead = head;
        priority_queue<ListNode*, vector<ListNode*>, Compare> pq;
        for(auto& i : lists){
            if(i != nullptr)
                pq.push(i);
        }
        while(!pq.empty()){
            head->next = pq.top();
            head = head -> next;
            if(pq.top()->next != nullptr){
                pq.push(pq.top()->next);
            }
            pq.pop();
        }
        

        return dummyhead->next;
    }
};
```





#### Merge Sort

TC: O(Nlogk)

SC: O(1) + O(logk) on stack

```
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
    ListNode* mergeKLists(vector<ListNode*>& lists) {
        if(lists.empty()){
            return nullptr;
        }
        return mergeKListsHelper(lists, 0, lists.size()-1);
    }
    ListNode* mergeKListsHelper(vector<ListNode*> lists, int start, int end){
        if(start == end){
            return lists[start];
        }
        if(start + 1 == end){
            return merge(lists[start], lists[end]);
        }
        int mid = start + (end - start) / 2;
        ListNode* left = mergeKListsHelper(lists, start, mid);
        ListNode* right = mergeKListsHelper(lists, mid+1, end);
        return merge(left, right);
    }
    ListNode* merge(ListNode* left, ListNode* right){
        ListNode* head = new ListNode(0);
        ListNode* dummyhead = head;
        while(left != nullptr && right != nullptr){
            if(left -> val < right -> val){
                head -> next = left;
                head = head->next;
                left = left -> next;
            }else{
                head ->next = right;
                head = head->next;
                right = right->next;
            }
        }
        if(left != nullptr){
            head -> next = left;
        }
        if(right != nullptr){
            head -> next = right;
        }
        return dummyhead->next;
    }
};
```


