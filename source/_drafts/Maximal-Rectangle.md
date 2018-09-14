title: Maximal Rectangle
author: Halfopen
tags:
  - leetcode
  - hard
categories:
  - 刷题
date: 2018-08-12 11:08:00
---
### [85\. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/)

Difficulty: **Hard**



Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

**Example:**

```
**Input:**
[
  ["1","0","1","0","0"],
  ["1","0","**1**","**1**","**1**"],
  ["1","1","**1**","**1**","**1**"],
  ["1","0","0","1","0"]
]
**Output:** 6
```

https://www.youtube.com/watch?v=g8bSdXCG-lA　


按行或者列扫描，每一行当作求连续矩形中的最大矩形面积的子问题
对于第一个元素，如果是０，赋值为０，如果是１，则加１

#### Solution

Language: **C++**

```c++
class Solution {
public:
    int maximalRectangle(vector<vector<char>>& matrix) {
        
    }
};
```