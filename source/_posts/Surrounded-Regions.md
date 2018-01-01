title: Surrounded Regions
author: Halfopen
tags:
  - leetcode
  - medium
  - 搜索
categories:
  - 刷题
date: 2018-01-01 14:25:00
---
### [130\. Surrounded Regions](https://leetcode.com/problems/surrounded-regions/description/)

Difficulty: **Medium**

Given a 2D board containing `'X'` and `'O'` (the **letter** O), capture all regions surrounded by `'X'`.

A region is captured by flipping all `'O'`s into `'X'`s in that surrounded region.

For example,  

```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:

```
X X X X
X X X X
X X X X
X O X X
```

#### Solution
```java
class Solution {
    int[][] d = {{0,1}, {0,-1}, {1,0}, {-1,0}};
    public void solve(char[][] board) {
        if(null==board)return;
        if(board.length==0)return;
        if(board[0].length==0)return;
        
        int m = board.length;
        int n = board[0].length;
        int[][] v = new int[m][n];
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if(board[i][j]=='O' && (i==0||i==m-1||j==0||j==n-1)){
                    board[i][j] = '1';
                    Queue<Integer> q = new LinkedList<>();
                    q.add(i*n+j);
                    while(!q.isEmpty()){	// 用递归容易爆内存
                        int cur = q.poll();
                        int x = cur/n;
                        int y = cur%n;
                        for(int[] di:d){
                            int dx = x+di[0];
                            int dy = y+di[1]; //这里不要写错
                            if(check(dx, dy, m, n) && board[dx][dy]=='O'){
                                q.add(dx*n+dy);
                                board[dx][dy]='1';
                            }
                        }
                    }// end of while
                }
            }
        }
        // 还原标记
        for(int i=0;i<m;i++){
            for(int j=0;j<n;j++){
                if (board[i][j]=='O') {
                    board[i][j]='X';
                } else if (board[i][j]=='1') {
                    board[i][j]='O';
                }
            }
        }
    }
    
    public boolean check(int x, int y, int m, int n){
        return x>=0&& x<m && y>=0 && y<n;
    }
    
}
```