title: Search a 2D Matrix II
author: Halfopen
tags:
  - leetcode
categories:
  - 刷题
date: 2018-03-20 09:12:00
---
### [240\. Search a 2D Matrix II](https://leetcode.com/problems/search-a-2d-matrix-ii/description/)

Difficulty: **Medium**



Write an efficient algorithm that searches for a value in an _m_ x _n_ matrix. This matrix has the following properties:

*   Integers in each row are sorted in ascending from left to right.
*   Integers in each column are sorted in ascending from top to bottom.

For example,

Consider the following matrix:

```
[
  [1,   4,  7, 11, 15],
  [2,   5,  8, 12, 19],
  [3,   6,  9, 16, 22],
  [10, 13, 14, 17, 24],
  [18, 21, 23, 26, 30]
]
```

Given **target** = `5`, return `true`.

Given **target** = `20`, return `false`.



#### Solution
从右上角开始，target比它小就向左，target比它大就向下
直到遇到边界。
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