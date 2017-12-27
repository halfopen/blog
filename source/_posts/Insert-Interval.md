title: Insert Interval
author: Halfopen
tags:
  - leetcode
  - hard
categories:
  - 刷题
date: 2017-12-26 14:03:00
---
### [57\. Insert Interval](https://leetcode.com/problems/insert-interval/description/)

Difficulty: **Hard**

Given a set of _non-overlapping_ intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

**Example 1:**  
Given intervals `[1,3],[6,9]`, insert and merge `[2,5]` in as `[1,5],[6,9]`.

**Example 2:**  
Given `[1,2],[3,5],[6,7],[8,10],[12,16]`, insert and merge `[4,9]` in as `[1,2],[3,10],[12,16]`.

This is because the new interval `[4,9]` overlaps with `[3,5],[6,7],[8,10]`.

区间合并，并且输入的区间是不重叠的

#### Solution
两个区间i,j的位置有 ss si sb ii ib bb,水题


```java
/**
 * Definition for an interval.
 * public class Interval {
 *     int start;
 *     int end;
 *     Interval() { start = 0; end = 0; }
 *     Interval(int s, int e) { start = s; end = e; }
 * }
 */
class Solution {
    public List<Interval> insert(List<Interval> intervals, Interval newInterval) {
        List<Interval> list = new ArrayList<>();
        boolean flag = true;
        for(Interval i: intervals){
            // s i
            if(i.start<newInterval.start && i.end>=newInterval.start && i.end<=newInterval.end){
                newInterval.start = i.start;
            }
            
            // i b
            if(i.start>=newInterval.start&& i.start<=newInterval.end && i.end>newInterval.end){
                newInterval.end = i.end;
            }
            
            // s b
            if(i.start<newInterval.start && i.end>newInterval.end){
                flag = false;
                list.add(i);
            }
            // i i

            // s s
            if(i.end<newInterval.start){
                list.add(i);
            }
            
            // b b            
            if(i.start>newInterval.end){
                if(flag==true){
                    list.add(newInterval);
                    flag=false;
                }
                list.add(i);
            }
        }
        if(flag==true){
            list.add(newInterval);
        }
        return list;
    }
}
```