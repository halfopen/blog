title: Word Search
author: Halfopen
tags:
  - dfs
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-08-15 22:28:00
---
### [79\. Word Search](https://leetcode.com/problems/word-search/description/)

Difficulty: **Medium**



Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "**ABCCED**", return **true**.
Given word = "**SEE**", return **true**.
Given word = "**ABCB**", return **false**.
```



#### Solution

Language: **Java**

```java
class Solution {
    public boolean exist(char[][] board, String word) {
        if(null==board || board.length==0)return false;
        
        int h = board.length;
        int w = board[0].length;
        
        
        boolean flag = false;
        for(int i=0;i<h&&flag==false;i++){
            for(int j=0;j<w&&flag==false;j++){
                if(board[i][j]==word.charAt(0)){
                    int[][] visited = new int[h][w];
                    //System.out.println("find start:"+i+" "+j);
                    if(dfs(board, visited, i, j, word, 0)){
                        flag = true;
                        break;
                    }
                }
            }
        }
        
        return flag;
    }
    
    public boolean dfs(char[][] board, int[][] visited, int i, int j, String word, int pos){
        // 退出条件
        int h = visited.length;
        int w = visited[0].length;
        if(pos>=word.length())return true;
        if(i<0||i>=h||j<0||j>=w)return false;
        
        if(visited[i][j]==1)return false;
        
        // 如果当前匹配正确
        if(word.charAt(pos) == board[i][j]){
            visited[i][j] = 1;
            //System.out.println("find "+board[i][j]+i+" "+j+" ");
            
            // 四个方向继续
            if(dfs(board, visited, i, j+1, word, pos+1))return true;
            if(dfs(board, visited, i, j-1, word, pos+1))return true;
            if(dfs(board, visited, i+1, j, word, pos+1))return true;
            if(dfs(board, visited, i-1, j, word, pos+1))return true;
            
            // 如果四个方向都没有找到，还原
            visited[i][j] = 0;
        }
        return false;      
    }
}
```