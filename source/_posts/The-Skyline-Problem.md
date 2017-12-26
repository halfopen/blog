title: The Skyline Problem
author: Halfopen
tags:
  - leetcode
  - hard
  - 线段树
categories:
  - 刷题
date: 2017-12-25 22:01:00
---
### [218\. The Skyline Problem](https://leetcode.com/problems/the-skyline-problem/description/)

Difficulty: **Hard**

A city's skyline is the outer contour of the silhouette formed by all the buildings in that city when viewed from a distance. Now suppose you are **given the locations and height of all the buildings** as shown on a cityscape photo (Figure A), write a program to **output the skyline** formed by these buildings collectively (Figure B).
<img src="https://leetcode.com/static/images/problemset/skyline1.jpg" width = "300" height = "200"  align=center />
<img src="https://leetcode.com/static/images/problemset/skyline2.jpg" width = "300" height = "200"  align=center />

The geometric information of each building is represented by a triplet of integers `[Li, Ri, Hi]`, where `Li` and `Ri` are the x coordinates of the left and right edge of the ith building, respectively, and `Hi` is its height. It is guaranteed that `0 ≤ Li, Ri ≤ INT_MAX`, `0 < Hi ≤ INT_MAX`, and `Ri - Li > 0`. You may assume all buildings are perfect rectangles grounded on an absolutely flat surface at height 0.

For instance, the dimensions of all buildings in Figure A are recorded as: `[ [2 9 10], [3 7 15], [5 12 12], [15 20 10], [19 24 8] ]` .

The output is a list of "**key points**" (red dots in Figure B) in the format of `[ [x1,y1], [x2, y2], [x3, y3], ... ]` that uniquely defines a skyline. **A key point is the left endpoint of a horizontal line segment**. Note that the last key point, where the rightmost building ends, is merely used to mark the termination of the skyline, and always has zero height. Also, the ground in between any two adjacent buildings should be considered part of the skyline contour.

For instance, the skyline in Figure B should be represented as:`[ [2 10], [3 15], [7 12], [12 0], [15 10], [20 8], [24, 0] ]`.

**Notes:**

*   The number of buildings in any input list is guaranteed to be in the range `[0, 10000]`.
*   The input list is already sorted in ascending order by the left x position `Li`.
*   The output list must be sorted by the x position.
*   There must be no consecutive horizontal lines of equal height in the output skyline. For instance, `[...[2 3], [4 5], [7 5], [11 5], [12 7]...]` is not acceptable; the three lines of height 5 should be merged into one in the final output as such: `[...[2 3], [4 5], [12 7], ...]`



#### Solution
直接暴力枚举会超时，思路和 https://briangordon.github.io/2014/08/the-skyline-problem.html 一开始想的一样。
```java
class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> list = new ArrayList<>();
        TreeMap<Integer, Integer> map = new TreeMap<>();
        
        for(int i=0;i<buildings.length;i++){
            int[] b = buildings[i];
            for(int j=b[0];j<=b[1];j++){
                int h = map.getOrDefault(j, 0);
                if(b[2]>=h){
                    map.put(j, b[2]);
                }
            }
        }
        
        int lastHeight=-1, lastPosition=-1;
        Iterator iter = map.entrySet().iterator();
        boolean isFirst=true;
        while(iter.hasNext()) {
            Map.Entry entry = (Map.Entry)iter.next();
            int key = (Integer)entry.getKey();
            int value = (Integer)entry.getValue();

            if(isFirst){
                lastHeight=value;
                lastPosition=key;
                int[] point1 = {key, value};
                list.add(point1);
                isFirst=false;
                continue;
            }else if(!iter.hasNext()){
                int[] point1 = {key, 0};
                list.add(point1);
                continue;
            }
            
            if(lastPosition+1!=key){
                int[] point1 = {lastPosition, 0};
                list.add(point1);
                int[] point2 = {key, value};
                list.add(point2);
            }else if(lastHeight>value){
                int[] point1 = {key-1, value};
                list.add(point1);
            }else if(lastHeight<value){     
                
                int[] point1 = {key, value};
                list.add(point1);
            }
            
            
            lastHeight=value;
            lastPosition=key;
        }
        return list;
    }
}
```


用队列保存当前可比较的高度，优先队列第一条就是最高的高度，然后，左边的边高度可以一直延续到右边
因此把左边的高度标记为负数。

```java
class Solution {
    public List<int[]> getSkyline(int[][] buildings) {
        List<int[]> list = new ArrayList<>();
        List<int[]> heights = new ArrayList<>();
        Queue<Integer> pq = new PriorityQueue<>((a, b) -> (b - a));
        for(int[] b :buildings){
            heights.add(new int[]{b[0], -b[2]}); // mark left 
            heights.add(new int[]{b[1], b[2]});
        }
        
        Collections.sort(heights, (a, b)->{
            if(a[0]!=b[0])return a[0] -b[0];
            return a[1] - b[1];
        });
            
        int pre = 0;
        pq.offer(0);
        
        for(int[] h: heights){
            int height = h[1];
            if(height<0){
                pq.offer(-height);  // left should be add to pq
            }else{  
                pq.remove(height);  // left is end by right
            }
            // get current max height
            int cur = pq.peek();
            
            if(cur!= pre){   // if current height is not the max height
                list.add(new int[]{h[0], cur});
                pre = cur;
            }
        }
        
        return list;
    }
}
```