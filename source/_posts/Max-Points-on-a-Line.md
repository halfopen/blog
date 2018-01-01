title: Max Points on a Line
author: Halfopen
tags:
  - leetcode
  - hard
categories:
  - 刷题
date: 2017-12-30 17:26:00
---
### [149\. Max Points on a Line](https://leetcode.com/problems/max-points-on-a-line/description/)

Difficulty: **Hard**

Given _n_ points on a 2D plane, find the maximum number of points that lie on the same straight line.

给出一堆二维的点，求出在同一条线上的点的最多个数。

#### Solution

pi pj就可以构成一个线，因此，所有的线一共有n*(n-1)种，判断的时候，每次要全部遍历，因此时间复杂度为O(n^3)

```java
/**
 * Definition for a point.
 * class Point {
 *     int x;
 *     int y;
 *     Point() { x = 0; y = 0; }
 *     Point(int a, int b) { x = a; y = b; }
 * }
 */
class Solution {
    
    
    static class Line{
        int sx;
        int sy;
        int ex;
        int ey;
        HashSet<Integer> pi = new HashSet<>();
        Line(){sx=0;sy=0;ex=0;ey=0;}
        
        Line(int x1,int y1, int x2, int y2){
            sx=x1;sy=y1;ex=x2;ey=y2;
        }
        
        public boolean inLine(int x, int y){
        	// 两个点重合
            if(sx==ex && sy==ey){
                return sx==x&&y==ey;
            }
            float a = sx-ex;
            float b = sy-ey;
            
            float a2 = x-ex;
            float b2 = y-ey;
            
            if(b==0&&b2==0)return true;
            
            
            return a*b2==b*a2;
        }
    }
    
    public int maxPoints(Point[] points) {
        if(null==points)return 0;
        if(points.length<=1)return points.length;
        int len = points.length;
        
        
        List<Line> lines = new ArrayList<>();
        HashMap<String, String> same = new HashMap<>();
        int max = 0;
        
        for(int i=0;i<len-1;++i){
            for(int j=i+1;j<len;j++){
                Point p1 = points[i];
                Point p2 = points[j];
                
                boolean isInLine = false;
                
                for(Line l: lines){
                    // 如果两个端点都在直线上
                    if(l.inLine(p1.x, p1.y) && l.inLine(p2.x, p2.y) && !l.pi.contains(i) && !l.pi.contains(j)){
                        l.pi.add(i);
                        l.pi.add(j);
                        isInLine = true;
                        break;
                    // 如果p1在直线上并且不是端点
                    }else if(l.inLine(p1.x, p1.y) && !l.pi.contains(i)){
                        l.pi.add(i);
                    }else if(l.inLine(p2.x, p2.y) && !l.pi.contains(j)){
                        l.pi.add(j);
                    }
                }
                
                if(!isInLine){
                    Line line = new Line(p1.x, p1.y, p2.x, p2.y);
                    line.pi.add(i);
                    line.pi.add(j);
                    lines.add(line);
                }
            }
        }

        for(Line l: lines){
            max = l.pi.size()>max?l.pi.size():max;
        }
        return max;
    }
}
```

这样的做法会超时

```java

public class Solution {
    
    private int gcd(int a, int b) {
        if ( a==0 ) return b;
        return gcd ( b%a, a );
    }
    
    public int maxPoints(Point[] points) {
        if(points.length <= 0) return 0;
        if(points.length <= 2) return points.length;
        int result = 0;
        for(int i = 0; i < points.length; i++){
            Map<String, Integer> hm = new HashMap<>();
            int samex = 1;
            int samey = 1;
            int samep = 0;
            // 
            for(int j = 0; j < points.length; j++){
                if(j != i) {
                	// 统计和点[i]相同的点
                    if((points[j].x == points[i].x) && (points[j].y == points[i].y))
                        samep++;
                    // 统计和点[i] x坐标相同的点 斜率不存在的一条线
                    if(points[j].x == points[i].x){
                        samex++;
                        continue;
                    }
                    // 统计和点[i] y坐标相同的点 斜率是0的一条线
                    if(points[j].y == points[i].y) {
                        samey++;
                        continue;
                    }
                    int numerator = points[j].y - points[i].y;
                    int denaminator = points[j].x - points[i].x;
                    int gcd = gcd(numerator, denaminator);
                    String hashStr = (numerator/gcd) + "_" + (denaminator/gcd); // 保存向量
                    hm.put(hashStr,hm.getOrDefault(hashStr, 1) + 1);
                    result = Math.max(result, hm.get(hashStr) + samep);
                }
            }
            result = Math.max(result, Math.max(samex, samey));
        }
        return result;
    }
}
```
