# Binary Search

## Use as

1. 数组有序

## Principles

1. 确保搜索范围减少，保证每次循环至少排出掉一个
2. 确保正确答案不会被排除

## Interview

1. Clarification （和面试官确认）
    1. 数组是否有序 sorted
    2. 升序降序 ascending
    3. 是否为空 null
    4. 重复元素 duplicate
2. Examples （再次确认题目）
3. Solution
    1. Assumptions
        1. null or size == 0 return ?
        2. duplicate return which one
        3. no answer return ? -1
    2. Signature
        1. function name
        2. input: int[], int (array, target)
        3. output: int (index)
    3. High Level Algorithm Description
        1. Binary Search (对于复杂的算法，解释使用什么样的数据结构，什么算法)
    4. Corner case
        1. null, empty
    5. Time/Space Complexity
        1. Time: O(logN)
        2. Space: O(1)
4. Test
    1. Test corner cases: null, empty/0, 1, 2 elements
    2. Test general cases

## Find Target

```cpp
int binarySearch(vector<int> nums, int target){
	int left = 0;
	int right = nums.size() - 1;
	while(left <= right){
	    int mid = (left + right) / 2;
	    if(nums[mid] == target)
	        return ....;
	    else if(nums[mid] < target){
	        left = .....;
	    }
	    else if(nums[mid[ > target){
	        right = .....;
	    }
	  }
}
```

<aside>
💡 mid 参数更新 使用 left + (right - left) / 2 来规避超出范围的问题

</aside>

<aside>
💡 为什么while循环中的条件是 <= 而不是 <

因为right初始化为nums.size()-1，是最后一个元素的索引。这两个条件可能出现在不同功能的二分搜索中。

1. 对于<=，适用于[left, right]区间
2. 对于<，适用于[left, right)区间
</aside>

## Closest In Sorted Array

1. Clarfication
    1. sorted? ascending?
    2. 2 closest? any? 
2. Examples
3. Solution
    1. Assumptions
        1. empty, null
    2. Signature
        1. input (int[] array, int target)
        2. output (int ans)
    3. High Level Algorithm
        1. Binary Search
    4. Time/Space Complexity
        1. Time: O(logn)
        2. Space: O(1)
    5. Corner cases
        1. null
        2. empty
4. Test
    1. Explain the corner case can be handle at which line

```java
public static int closestElement(int[] array, int target){
	if(array == null || array.length == 0){
		return -1;
	int left = 0;
	int right = array.length - 1;
	while (left < right - 1){
		int mid = left + ( right - left ) / 2;
		if (array[mid] == target){
			return mid;
		}
		else if(array[mid] < target){
			left = mid;
		}
		else{
			right = mid;
		}
	}
	if (Math.abs(array[left] - target) < Math.abs(array[right] - target)){
		reutrn left;
	}
	else{
		return right;
	}
}
```

java 中为什么要把数组声明为null

## K Closet In Sorted Array

1. Clarification
    1. sorted? ascending?
    2. duplicate? any
    3. multiple solution? any
    4. K > array.length ?
2. Examples
3. Solution
    1. Assumptions
        1. empty, null
    2. Signature
        1. input (int[] array, int target, int K)
        2. output (int ans)
    3. High Level Algorithm
        1. Binary Search find the closest number
        2. Expand to K closest
    4. Time/Space Complexity
        1. Time: O(n)
        2. Space: O(1)
    5. Corner cases
        1. null
        2. empty