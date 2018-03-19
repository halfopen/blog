title: Kth Smallest Element in a Sorted Matrix
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-03-18 19:56:00
---
### [378\. Kth Smallest Element in a Sorted Matrix](https://leetcode.com/problems/kth-smallest-element-in-a-sorted-matrix/description/)

Difficulty: **Medium**



Given a _n_ x _n_ matrix where each of the rows and columns are sorted in ascending order, find the kth smallest element in the matrix.

Note that it is the kth smallest element in the sorted order, not the kth distinct element.

**Example:**

```
matrix = [
   [ 1,  5,  9],
   [10, 11, 13],
   [12, 13, 15]
],

每一行和每一列都是递增的，matrix大小是nxn的。
k = 8,

return 13.
```

**Note:**  
You may assume k is always valid, 1 ≤ k ≤ n<sup>2</sup>.



#### Solution

右下角肯定是最大的，比如  
1,2,
10,11  11是最大的，而15是所有数中最大的

思路一：从右下角进行层次遍历，每次只向左和向上遍历
比如找到15是最大的，那些下一次出现最大的数也有可能在15的左边或者上边
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int[][] visited = new int[n][n];
        
        List<Integer> queue = new ArrayList<>(n*n);
        int x=n-1,y = n-1;
        int count = 0;
        queue.add(x*n+y); // 添加初始的最大值
        visited[x][y] = 1;
        int result = matrix[x][y];
        while(count<=n*n-k){
            // 遍历queue找出最小的数,queue存的是x*n+y
            int max = Integer.MIN_VALUE;
            int maxIndex = 0;
            for(int i=0;i<queue.size();i++){
                int num = queue.get(i);
                int cx = num/n;
                int cy = num%n;
                if(max<= matrix[cx][cy]){
                    maxIndex = i;
                    max = matrix[cx][cy];
                }
            }
            
            // 移除最大的那一个，并把它的左和上添加
            int pos = queue.get(maxIndex);
            
            queue.remove(maxIndex);
            count++;
            result = matrix[pos/n][pos%n];
            
            //System.out.println(pos+" "+" "+(pos/n)+" "+(pos%n)+" "+result);
            int left = pos - 1;
            int top = pos - n;
            
            int cx = left/n;
            int cy = left%n;
            if(left>=0 && visited[cx][cy]==0){
                queue.add(left);
                visited[cx][cy] = 1;
            }
            cx = top/n;
            cy = top%n;
            if(top>=0 && visited[cx][cy]==0){
                queue.add(top);
                visited[cx][cy] = 1;
            }
            
            //System.out.println(queue);
        }
        return result;
        
    }
}
```

思路二，discuss中的二分查找法

```java

class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int m = matrix.length - 1 ;
        int n = matrix[0].length - 1 ;
        int lo = matrix[0][0];
        int hi = matrix[m][n] ;
        while (lo < hi) {
            int mid = lo + (hi - lo) / 2 ;
            int cnt = countNum(matrix, mid);
            if (cnt < k) {
                lo = mid + 1 ;
            } else{
                hi = mid ;
            }
        }
        return lo;
    }
    
    
    private int countNum (int[][] matrix, int val){
        int n = matrix[0].length -  1 ;
        int i = 0 , j = n ;
        int count = 0 ;
        while (i < matrix.length) {
            while (j >= 0 && matrix[i][j] > val) j-- ;
            count += j + 1 ;
            i++;
        }            
        return count ;
    }
}
```

思路三 用堆结构，和第一种方法思路差不多，pq中保存有可能最小的数，下一个可能最小的数就应该包括当前数字的下方

    初始化 pq = 1 5 9
    取1  pq = 5 9 10
    取5  pq = 9 10 11
    取9  pq = 10 11 13
    取10 pq = 11 12 13
    取11 pq = 12 13 13
    取12 pq = 13 13
    取13 pq = 13
    取13 pq = 15
    取15 pq = null
    ... 
    

```java
public class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        PriorityQueue<Tuple> pq = new PriorityQueue<Tuple>();
        for(int j = 0; j <= n-1; j++) pq.offer(new Tuple(0, j, matrix[0][j]));
        for(int i = 0; i < k-1; i++) {
            Tuple t = pq.poll();
            if(t.x == n-1) continue;
            pq.offer(new Tuple(t.x+1, t.y, matrix[t.x+1][t.y]));
        }
        return pq.poll().val;
    }
}

class Tuple implements Comparable<Tuple> {
    int x, y, val;
    public Tuple (int x, int y, int val) {
        this.x = x;
        this.y = y;
        this.val = val;
    }
    
    @Override
    public int compareTo (Tuple that) {
        return this.val - that.val;
    }
}
```



思路四 直接用系统的排序方法，感觉和直接用sort方法差不多
```java
class Solution {
    public int kthSmallest(int[][] matrix, int k) {
        int n = matrix.length;
        int[] array = new int[n*n];
        for(int i=0;i<n;i++){
            for(int j=0;j<n;j++){
                array[i*n+j] = matrix[i][j];
            }
        }
        Arrays.sort(array);
        return array[k-1]; 
    }
}
```