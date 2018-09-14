title: Set Matrix Zeroes
author: Halfopen
tags:
  - leetcode
  - medium
categories:
  - 刷题
date: 2018-09-13 13:16:00
---
### [73\. Set Matrix Zeroes](https://leetcode.com/problems/set-matrix-zeroes/description/)

Difficulty: **Medium**



Given a _m_ x _n_ matrix, if an element is 0, set its entire row and column to 0\. Do it .

**Example 1:**

```
**Input:** 
[
  [1,1,1],
  [1,0,1],
  [1,1,1]
]
**Output:** 
[
  [1,0,1],
  [0,0,0],
  [1,0,1]
]
```

**Example 2:**

```
**Input:** 
[
  [0,1,2,0],
  [3,4,5,2],
  [1,3,1,5]
]
**Output:** 
[
  [0,0,0,0],
  [0,4,5,0],
  [0,3,1,0]
]
```

**Follow up:**

*   A straight forward solution using O(_m__n_) space is probably a bad idea.
*   A simple improvement uses O(_m_ + _n_) space, but still not the best solution.
*   Could you devise a constant space solution?



#### Solution

Language: **Java**
把第一列和第一行作为标记，如果为０表示这一行或者这一列要设置为０，此外，第一行和第一列本身是否有０用两个变量标记．
```java
class Solution {
    public void setZeroes(int[][] matrix) {
        boolean fr = false,fc = false;
        for(int i = 0; i < matrix.length; i++) {
            for(int j = 0; j < matrix[0].length; j++) {
                if(matrix[i][j] == 0) {
                    if(i == 0) fr = true;
                    if(j == 0) fc = true;
                    matrix[0][j] = 0;
                    matrix[i][0] = 0;
                }
            }
        }
        for(int i = 1; i < matrix.length; i++) {
            for(int j = 1; j < matrix[0].length; j++) {
                if(matrix[i][0] == 0 || matrix[0][j] == 0) {
                    matrix[i][j] = 0;
                }
            }
        }
        if(fr) {
            for(int j = 0; j < matrix[0].length; j++) {
                matrix[0][j] = 0;
            }
        }
        if(fc) {
            for(int i = 0; i < matrix.length; i++) {
                matrix[i][0] = 0;
            }
        }
    }
}
```