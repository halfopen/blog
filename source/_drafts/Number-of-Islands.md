title: Number of Islands
author: Halfopen
tags:
  - 并查集
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-23 20:56:00
---
### [200\. Number of Islands](https://leetcode.com/problems/number-of-islands/description/)

Difficulty: **Medium**



Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

_**Example 1:**_

```
11110  
11010  
11000  
00000```

Answer: 1

_**Example 2:**_

```
11000  
11000  
00100  
00011```

Answer: 3



#### Solution
直接dfs
```java
class Solution {
    int c = 0;
    int w, h;
    int[][] v;
    public int numIslands(char[][] grid) {
        int count = 0;
        if(null == grid)return count;
        if(grid.length==0)return count;
        
        h = grid.length;
        w = grid[0].length;
        v = new int[h][w];
        
        for(int i=0;i<h;i++){
            for(int j=0;j<w;j++){
                if(v[i][j]==0 && grid[i][j]=='1'){
                    dfs(i, j, grid);
                    count++;
                }
            }
        }
        return count;
    }
    
    public void dfs(int i, int j, char[][] grid){
        if(!check(i, j))return ;
        if(grid[i][j]=='0' || v[i][j]!=0)return ;
        
        v[i][j]=1;
        dfs(i+1, j, grid);
        dfs(i-1, j, grid);
        dfs(i, j+1, grid);
        dfs(i, j-1, grid);
    }
    
    public boolean check(int i, int j){
        if(i>=0&& i<h && j>=0&& j<w)return true;
        return false;
    }
}
```