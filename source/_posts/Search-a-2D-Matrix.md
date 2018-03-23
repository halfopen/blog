title: Search a 2D Matrix
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-20 09:47:00
---
### [74\. Search a 2D Matrix](https://leetcode.com/problems/search-a-2d-matrix/description/)

Difficulty: **Medium**



Write an efficient algorithm that searches for a value in an _m_ x _n_ matrix. This matrix has the following properties:

*   Integers in each row are sorted from left to right.
*   The first integer of each row is greater than the last integer of the previous row.

For example,

Consider the following matrix:

```
[
  [1,   3,  5,  7],
  [10, 11, 16, 20],
  [23, 30, 34, 50]
]
```

Given **target** = `3`, return `true`.



#### Solution
可以用 [Search-a-2D-Matrix-II](2018/03/20/Search-a-2D-Matrix-II/)一样的代码通过
```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix==null)return false;
        if(matrix.length==0)return false;
        if(matrix[0].length==0)return false;
        int m = matrix.length;
        int n = matrix[0].length;
        
        int x = 0, y = n-1;
        
        while(matrix[x][y]!= target){ 
            if(matrix[x][y]> target){
                if(--y<0)return false;
            }else{
                if(++x>=m)return false;
            }
        }
        return true;
    }
}
```

直接当做一维进行二分查找
```java
class Solution {
public:
    bool searchMatrix(vector<vector<int> > &matrix, int target) {
        int n = matrix.size();
        int m = matrix[0].size();
        int l = 0, r = m * n - 1;
        while (l != r){
            int mid = (l + r - 1) >> 1;
            if (matrix[mid / m][mid % m] < target)
                l = mid + 1;
            else 
                r = mid;
        }
        return matrix[r / m][r % m] == target;
    }
};
```

leetcode上最快的代码,顺序查找O(n)，但是加了一个判断,对于false的情况能提前返回

```java
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        //slower method 1
        for (int r= 0; r < matrix.length; r++){
            for (int c = 0; c  < matrix[r].length; c++)
                if (matrix[r][c] > target)
                    return false;
                else if(matrix[r][c] == target)
                    return true;
        }
        return false;
        
    }
}
```
