title: Mission Improbable
author: Halfopen
tags:
  - 二分图
categories:
  - 刷题
date: 2017-12-05 15:38:00
---
# 4950: [Wf2017]Mission Improbable
Time Limit: 1 Sec Memory Limit: 1024 MB 


## 题目
[Mission Improbable原题链接](https://online.acmicpc.org/problems/improbable )


![upload successful](\assets\images\Mission Improbable\pasted-0.png)
大概意思就是有一堆箱子，在保持最终三视图不变的情况下，求出最多能移走多少个箱子


## Input

第一行包含两个整数r(1≤r≤100)和c(1≤n≤100),分别表示网格的行数与列数。 
接下来r行,每行包含c个整数,表示对应行上每堆立方体箱的高度(箱子的数量)。 
所有的高度在0到10^9之间 (含边界) 。

## Output

输出在不被发现的情况下最多能偷走多少箱子。

## Sample Input

1.in

    5 5 
    1 4 0 5 2 
    2 1 2 0 1 
    0 2 3 4 4 
    0 3 0 3 1 
    1 2 2 1 1

2.in

    2 3 
    50 20 3 
    20 10 3

## Sample Output

1.out

    9

2.out

    30

## 思路
以2.in为例
1、首先，把所有箱子都移走。

    0 0 0
    0 0 0

2、对于俯视图，我们要保证有箱子的地方不能为空，因此在不为空的位置，都放上一个箱子

    1 1 1
    1 1 1

3、把行和列的最大值位置箱子放上去

    50 20 3
    20 1  1

4、遍历箱子，如果当前位置不为空，并且这个位置对应行和列的高度相同，说明放这个位置可以同时满足行和列的需求，只要放一次就行了，相当于3多放了一次，我们要尽可能地去重复，利用匈牙利算法去重，让横纵轴最多匹配一次。

    50 1  3
    1 20  1

5、对去重之后还剩下的重复点，把对应的箱子数加回来

## Python代码

```python
# -*- coding:utf-8 -*-
import numpy as np


class Solution:
    """
        ICPC 2007 Problem C 推箱子
    """
    def __init__(self, input_file):
        self.grid = None
        self.w = 0                  # 行数
        self.h = 0                  # 列数
        self.result = 0             # 结果
        self.line = []              # 所有边
        self.max_w = []             # 行的最大值
        self.max_h = []             # 列的最大值
        self.grid = []              # 字符串矩阵
        self.mat = None             # 数值矩阵
        self.right = set()          # 二分图右边
        self.right_matched = []     # 标记右侧是否已经被标记
        self.right_match = []       # 标记左边匹配的内容

        self.read_input(input_file)
        self.setup()

    def setup(self):
        """
            获取行列的最大值，把self.grid转为self.mat
            初始化变量
        :return: None
        """
        for i in range(self.w):
            for j in range(self.h):
                self.grid[i][j] = int(self.grid[i][j])
        self.mat = np.mat(self.grid)
        for i in range(self.w):
            self.max_w.append(self.mat[i, :].max())
            # print(self.mat[i, :].max())
        for j in range(self.h):
            self.max_h.append(self.mat[:, j].max())
            # print(self.mat[:, j].max())

        self.line = np.zeros((self.w, self.h))
        self.right_matched = [0]*(self.w+self.h)
        self.right_match = [-1]*(self.w + self.h)

    def read_input(self, input_file):
        """
            读取输入到grid中
        :param input_file:  输入文件路径
        :return: None
        """
        try:
            f = open(input_file, "r")
            first_line = f.readline().replace("\n", "")
            [w, h] = first_line.split(" ")

            self.w, self.h = int(w), int(h)
            self.grid = []
            assert self.w < 101 and self.h < 101
            for i in range(self.w):
                line = f.readline().replace("\n", "")
                self.grid.append(line.split(" "))

        except Exception as e:
            print(e)

    def mission_improbable(self):
        """
            解决推箱子问题
        :return: int 最多可移除的箱子数
        """
        # 遍历矩阵
        for i in range(self.w):
            for j in range(self.h):
                # 移走所有箱子
                self.result += self.mat[i, j]
                # 如果不为空
                if self.mat[i, j] > 0:
                    self.result -= 1     # 俯视图必须要留一块
                    # print("max",i,j, self.mat[i, j], self.max_w[i], self.max_h[j])
                    # 如果这个箱子的位置同时是行和列的最大值，添加到二分图中
                    if self.max_w[i] == self.max_h[j] and self.mat[i, j] > 1:
                        self.line[i, j] = 1
                        self.right.add(j)

        # print("全部移走", self.result)

        # 行的最大值不能移走
        for i in range(self.w):
            if self.max_w[i] > 0:
                self.result -= self.max_w[i]-1
        # 列的最大值不能移走
        for j in range(self.h):
            if self.max_h[j] > 0:
                self.result -= self.max_h[j]-1

        # print("移回行列最大", self.result)

        # 把最大匹配上的加回来
        for i in range(self.w):
            if self.max_w[i] > 0:
                self.right_matched = [0]*(self.w+self.h)
                if self.find(i):
                    # print("find ", i)
                    self.result += self.max_w[i] - 1
        return self.result

    def find(self, i):
        """
            匈牙利算法从i进行搜索
        :param i: 下标，从0开始
        :return: 左边的i是否有匹配
        """
        # 遍历右边
        for r in self.right:
            # print("check ",i," ", r, " ", self.line[i, r])
            if self.line[i, r] == 1 and self.right_matched[r] == 0:
                self.right_matched[r] = 1
                if self.right_match[r] == -1 or self.find(self.right_match[r]):
                    self.right_match[r] = i
                    return True
        return False


if __name__ == '__main__':
    print(Solution("./samples/1.in").mission_improbable())
    print(Solution("./samples/2.in").mission_improbable())


```

## 相关链接

[[1] 匈牙利算法](http://blog.csdn.net/dark_scope/article/details/8880547)
