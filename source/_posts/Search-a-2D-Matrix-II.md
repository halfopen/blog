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



http://bookshadow.com/weblog/2015/07/23/leetcode-search-2d-matrix-ii/

分治法，以矩形中点为基准，将矩阵拆分成左上，左下，右上，右下四个区域

若中点值 < 目标值，则舍弃左上区域，从其余三个区域再行查找

若中点值 > 目标值，则舍弃右下区域，从其余三个区域再行查找

时间复杂度递推式：T(n) = 3T(n/2) + c

相关博文：http://articles.leetcode.com/2010/10/searching-2d-sorted-matrix-part-ii.html
```
public class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        int n=matrix.length, m=matrix[0].length;
        return helper(matrix,0,n-1,0,m-1,target);
    }
    boolean helper(int[][] matrix, int rowStart, int rowEnd, int colStart, int colEnd, int target ){
        if(rowStart>rowEnd||colStart>colEnd){
            return false;
        }
        int rm=(rowStart+rowEnd)/2, cm=(colStart+colEnd)/2;
        if(matrix[rm][cm]== target){
            return true;
        }
        else if(matrix[rm][cm] >target){
            return helper(matrix, rowStart, rm-1,colStart, cm-1,target)||
                helper(matrix,  rm, rowEnd, colStart,cm-1,target) ||
                helper(matrix, rowStart, rm-1,cm, colEnd,target);
        }
        else{
            return helper(matrix, rm+1, rowEnd, cm+1,colEnd,target)||
                helper(matrix,  rm+1, rowEnd, colStart,cm,target) ||
                helper(matrix, rowStart, rm,cm+1, colEnd,target);
        }
    
}
```