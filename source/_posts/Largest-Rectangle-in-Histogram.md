title: Largest Rectangle in Histogram
author: Halfopen
tags:
  - leetcode
  - hard
  - 单调队列
categories:
  - 刷题
date: 2017-12-24 22:32:00
---
### [84\. Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/description/)
柱状图内最大的矩形面积

Difficulty: **Hard**

Given _n_ non-negative integers representing the histogram's bar height where the width of each bar is 1, find the area of largest rectangle in the histogram.

![](https://leetcode.com/static/images/problemset/histogram.png)  

Above is a histogram where width of each bar is 1, given height = `[2,1,5,6,2,3]`.

![](https://leetcode.com/static/images/problemset/histogram_area.png)  

The largest rectangle is shown in the shaded area, which has area = `10` unit.

For example,  
Given heights = `[2,1,5,6,2,3]`,  
return `10`.

这是一个很经典的面试题，求柱状图中的最大矩形面积。
用单调队列可以实现时间复杂度为O(n)

#### Solution

以上图为例，计算过程如下
s存的实际上是下标，这里为了直观，表示的是高度

	i=0 h=2 s=[ ],进到队列
    i=1 h=1 s=[2]比栈顶的2小，不满足单调队列，因此1要入队的话，要把前面的出队
    	2 出队，计算以2为高的面积。因为2往前最多可以到第一个比它低的柱状图，所以宽是当前的下标-前一个位置的下标-1。但是2出队之后队列为空，说明i之前的位置，最低高度是2，所以长度为i.面积为2*1=2
        i--,表示重新把h=1入队列
    i=2 h=5 s=[1],入队
    i=3 h=6 s=[1,5] 入队
    i=4 h=2 s=[1,5,6] 2比栈顶的6小，把6出队，计算6*（4-1-（前一个元素5的下标）2）=6
    				  2比栈顶的5小，把5出队，计算5* (4-1-(1的下标)1)=10
                      2比栈顶的1大,2入队
    i=5 h=3 s=[1,2], 入队
    i=6 h=0 s=[1,2,3]最后一个元素
    					3出队，计算3*(6-1-4)=3
    					2出队，计算2*(6-1-1)=8
                        1出队，1出队之后，队列为空，因此1是6个元素的最低，计算1*6=6
    面积最大为10
      
可以看出，在i的位置出队的时候，里面所有元素的高，长度都能算到i,因为是单调递增队列,已经出队的都比它高。


```java
public class Solution {
    public int largestRectangleArea(int[] height) {
        int len = height.length, h, former,area;
        Stack<Integer> s = new Stack<Integer>();
        int maxArea = 0;
        s.push(-1);
        for(int i=0;i<=len;++i){
            h = (i==len? 0 : height[i]);
            if(s.peek()<0 || h>=height[s.peek()]){
                s.push(i);
            }else{
                former = s.pop();
                maxArea = Math.max(height[former]*(i-1-s.peek()), maxArea);
                i--;
            }
        }
        return maxArea;
    }
}
```