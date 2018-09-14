title: Trapping Rain Water
author: Halfopen
tags:
  - leetcode
  - hard
categories:
  - 刷题
date: 2018-08-14 15:18:00
---
### [42\. Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/description/)

Difficulty: **Hard**



Given _n_ non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

![](http://www.leetcode.com/static/images/problemset/rainwatertrap.png)  
<small style="display: inline;">The above elevation map is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped. **Thanks Marcos** for contributing this image!</small>

**Example:**

```
**Input:** [0,1,0,2,1,0,1,3,2,1,2,1]
**Output:** 6```



#### Solution

Language: **Java**

    累加得到柱子面积 14
    先用一个递增队列，把上一个最高的柱子存起来
    然后遍历的时候，算出柱子加水的总面积
    1 1 2 2 2 2 3 2 2 2 1 = 20
    所以水面积＝20-14＝6

```java
class Solution {
    public int trap(int[] height) {
        int hArea= 0;
        int totalArea = 0;
        // 保存一个递减序列
        LinkedList<Integer> stack = new LinkedList<>();
        
        for(int i=0;i< height.length;i++){
            hArea += height[i];
            if(stack.isEmpty() || height[i]<height[stack.getLast()]){
                // 添加当前最高柱子的下标
                stack.addLast(i);
            }else{
                // 出现一个高的柱子
                while(!stack.isEmpty() && height[stack.getLast()]<=height[i]){
                    int last = stack.getLast();
                    for(int j=last+1;j<i;j++){
                        height[j] = height[last];
                    }
                    stack.removeLast();
                }
                if(!stack.isEmpty()){
                    int last = stack.getLast();
                    for(int j=last+1;j<i;j++){
                        height[j] = height[i];
                    }
                }
                stack.addLast(i);
            }
        }
        for(int i:height){
            totalArea+=i;
            System.out.print(i+ " ");
        }
        return totalArea - hArea;
    }
}
```

第二种算总面积的方法，用一个left和right从两边开始扫描，left递增，right递增，每次算新一层的面积

```java
class Solution {
    public int trap(int[] height) {
        int hArea= 0;
        int lastHeight = 0;
        
        int left = 0;
        int right = height.length-1;
        
        while(left<=right){
            // 如果左边的低
            if(height[left]<height[right]){
                if(height[left]>lastHeight){
                    //System.out.println(left+ " "+ right+" "+ lastHeight);
                    hArea += (height[left]-lastHeight)*(right-left+1);
                    lastHeight = height[left];
                }
                left++;
            }else{
                if(height[right]>lastHeight){
                    //System.out.println(left+ " "+ right+" "+ lastHeight);
                    hArea += (height[right]-lastHeight)*(right-left+1);
                    lastHeight = height[right];
                }
                right--;
            }
        }
        for(int i:height)hArea-=i;
        return hArea;
    }
}
```


