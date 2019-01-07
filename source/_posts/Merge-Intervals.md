title: Merge Intervals
author: Halfopen
tags:
  - medium
  - leetcode
categories:
  - 刷题
date: 2018-10-08 20:53:00
---
### [56\. Merge Intervals](https://leetcode.com/problems/merge-intervals/description/)

Difficulty: **Medium**



Given a collection of intervals, merge all overlapping intervals.

**Example 1:**

```
**Input:** [[1,3],[2,6],[8,10],[15,18]]
**Output:** [[1,6],[8,10],[15,18]]
**Explanation:** Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```

**Example 2:**

```
**Input:** [[1,4],[4,5]]
**Output:** [[1,5]]
**Explanation:** Intervals [1,4] and [4,5] are considerred overlapping.```



#### Solution

Language: **Java**

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
    public List<Interval> merge(List<Interval> intervals) {
        if (intervals.size() <= 1)
            return intervals;
        List<Interval> ret = new ArrayList<>();
        
        
        
        intervals.sort( (i1, i2)->{
           if(i1.start!=i2.start){
               return i1.start-i2.start;
           }
            return i1.end -i2.end;
        });
        
        int s = intervals.get(0).start;
        int e = intervals.get(0).end;
        
        for(Interval i:intervals){
            // System.out.println(i.start+" "+e);
            if(i.start<=e){  // 合并
                // 比较大小，更新 end
                e = Math.max(e, i.end);
            }else{ // 添加到ret
                ret.add(new Interval(s, e));
                s = i.start;
                e = i.end;
            }
        }
        // 添加最后一个
        ret.add(new Interval(s, e));
        
        return ret;
    }
}
```