# Search a 2D Matrix II

Data Structure: Array
Difficulty: Medium
Last Review Time: September 5, 2022 6:03 PM
No: 240

选择从左下角走，一定没有回头路

```cpp
class Solution {
public:
    bool searchMatrix(vector<vector<int>>& matrix, int target) {
        int size = matrix.size();
        int y_size = matrix[0].size();
        int x = 0;
        int y = y_size - 1;
        while(x < size && y>=0){
            int num = matrix[x][y];
            if(num == target)
                return true;
            if(num < target)
                ++x;
            else if(num > target){
                --y;
            }
        }
        return false;
    }
};
```

/i