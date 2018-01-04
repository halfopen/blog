title: Spiral Matrix
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-01-03 15:27:00
---
### [54\. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/)

Difficulty: **Medium**

Given a matrix of _m_ x _n_ elements (_m_ rows, _n_ columns), return all elements of the matrix in spiral order.

For example,  
Given the following matrix:

```
[
 [ 1, 2, 3 ],
 [ 4, 5, 6 ],
 [ 7, 8, 9 ]
]
```

You should return `[1,2,3,6,9,8,7,4,5]`.

#### Solution

定义四个方向，遇到不能前进就换方向，直到list的大小和数组元素大小相同。

```java
class Solution {
    
    public static int[][] d = new int[][]{ {0, 1}, {1,0}, {0, -1}, {-1, 0}};  // directions
    
    public List<Integer> spiralOrder(int[][] matrix) {
        if(null==matrix)return null;
        List<Integer> list = new ArrayList<>();
        int m = matrix.length;
        if(m<=0)return list;
        int n = matrix[0].length;
        
        int[][] visit = new int[m][n];
        int c = 0;      // start direction
        int dy = d[c][0], dx=d[c][1];
        int y=0,x=-1;   // start point
        
        while(list.size() <m*n){
            if(check(visit, y+dy, x+dx, m, n)){
                y += dy;
                x += dx;
                visit[y][x] = 1;

                list.add(matrix[y][x]);
            }else{  // change direction
                c = (c+1)%4;
                dy = d[c][0];
                dx = d[c][1];
            }
            

        }
        
        return list;
    }
    
    
    public boolean check(int[][] visit, int i, int j, int m, int n){
        if(i<0 || i>=m || j<0 || j>=n)return false;      
        if(visit[i][j]==1)return false;   
        return true;
    }
}
```