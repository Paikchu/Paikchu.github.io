# 278. 第一个错误的版本

Algorithm: 二分查找, 交互
Difficulty: Easy
Last Review Time: September 5, 2022 1:41 PM
No: 278

你是产品经理，目前正在带领一个团队开发新的产品。不幸的是，你的产品的最新版本没有通过质量检测。由于每个版本都是基于之前的版本开发的，所以错误的版本之后的所有版本都是错的。

假设你有 n 个版本 [1, 2, ..., n]，你想找出导致之后所有版本出错的第一个错误的版本。

你可以通过调用 bool isBadVersion(version) 接口来判断版本号 version 是否在单元测试中出错。实现一个函数来查找第一个错误的版本。你应该尽量减少对调用 API 的次数。

示例 1：

```cpp
输入：n = 5, bad = 4
输出：4
解释：
调用 isBadVersion(3) -> false
调用 isBadVersion(5) -> true
调用 isBadVersion(4) -> true
所以，4 是第一个错误的版本。
```

示例 2：

```cpp
输入：n = 1, bad = 1
输出：1
```

提示：

1 <= bad <= n <= 231 - 1

## 题目分析

[Binary Search](../Binary%20Search%20ff0a4476e7984442a09b45be293c7132.md)

## Code

### 2021 / 07 / 11

```cpp
class Solution {
public:
    int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        int mid;
        while(left<=right){
            mid = left + (right - left)/2;
            bool first = isBadVersion(mid);
            if(first){
                right = mid - 1;
            }
            else{
                left = mid + 1;
            }
        }
        return left;
    }
};
```

### 2021 / 07 / 11

当mid为bad version的时候，right更新后等于mid - 1，所以当循环结束的时候，left = right + 1 ，left为bad version的序号

```cpp
class Solution {
public:
    int firstBadVersion(int n) {
        int left = 1;
        int right = n;
        while(left<=right){
            int mid = left + (right - left)/2;
            if(isBadVersion(mid)){
                right = mid - 1;
            }
            else{
                left = mid + 1;
            }
        }
        return left;
    }
};
```

## 2022 / 04 / 07

考虑可能会存在找空的情况，创建了一个bad_v来记录，当前检测出得错误。结束循环之后，bad_v为最后检测出得一个bad_version。感觉不如第二个方法好。

```cpp
class Solution {
public:
    int firstBadVersion(int n) {
        // int mid = n / 2;
        int left = 1;
        int right = n;
        int bad_v = 1;
        while (left <= right){
            int mid = left + (right - left) / 2;
            if(isBadVersion(mid)){
                bad_v = mid;
                right = mid - 1;
            }
            else{
                left = mid + 1;
            }
        }
        return bad_v;
    }
};
```