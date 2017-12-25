title: Maximal Rectangle
author: Halfopen
tags:
  - leetcode
  - hard
categories:
  - 刷题
date: 2017-12-23 20:49:00
---
### [85\. Maximal Rectangle](https://leetcode.com/problems/maximal-rectangle/description/)

Difficulty: **Hard**

Given a 2D binary matrix filled with 0's and 1's, find the largest rectangle containing only 1's and return its area.

For example, given the following matrix:


1 0 1 0 0

1 0 <font color="red" style="display: inline;">1</font> <font color="red" style="display: inline;">1</font> <font color="red" style="display: inline;">1</font>

1 1 <font color="red" style="display: inline;">1</font> <font color="red" style="display: inline;">1</font> <font color="red" style="display: inline;">1</font>

1 0 0 1 0


Return 6.

求最大的矩形面积。

#### Solution

**思路1**：
一个矩形可以有左上角和右上角确定，暴力枚举左上角和右下角，然后检查是否是矩形

进一步限制条件，左上角的x y小于右下角x y,并且连通。

时间复杂度应该是(n*m)^2

其中，x1,y1-x2,y2是否为矩形，可以用map保存结果，提高效率。
**思路2**
一个矩形通过左上角，还有长和宽来确定。

1.选取一个左上角。
2.如果宽能增加，然后让宽增1。如果不能，回到1，选取下一个左上角。
3.以当前宽，尽可能把长增加。记录面积。回到2.

进一步优化，考虑矩形的包含关系，如果当前左上角和长宽确定的矩形在之前判断的矩形之内，肯定是比较小的，不用判断。
 因为有判断，所以可能快一点，但最大时间复杂度应该也是(n*m)^2

```java
class Solution {
    public int maximalRectangle(char[][] matrix) {
        if(null==matrix)return 0;
        if(matrix.length==0)return 0;
        
        int maxArea = 0;
        int h = matrix.length;
        int w = matrix[0].length;
        
        for(int i=0;i<h;++i){
            for(int j=0;j<w;++j){
                int area = 0;
                int minWidth = w-1;
                if(matrix[i][j]=='1'){
                    //System.out.println("check:"+i+" "+j);
                    area = 1;
                    for(int height=i;height<h && matrix[height][j]=='1';height++){
                        boolean flag = false;
                        for(int width=j;width<w;width++){
                            //System.out.println("extend:"+height+" "+width);
                            if(width>minWidth)break;
                            
                            if(matrix[height][width]=='0'){
                                if(width-1<minWidth)minWidth = width-1;
                                break;
                            }else{
                                flag = true;
                            }
                        }
                        area = (minWidth-j+1)*(height-i+1);
                        if(area>maxArea && flag){
                            System.out.println(i+" "+j+" "+minWidth+" "+height+" "+area);
                            maxArea = area;
                        }
                        
                    }
                    
                }
            }
        }
        return maxArea;
    }
}
```