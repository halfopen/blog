title: java对象自定义排序
author: Halfopen
tags:
  - java基础
categories:
  - java
date: 2018-03-24 21:14:00
---
```java
import java.util.*;

public class TT1{
    static class Point{
        public int x;
        public int y;
        public Point(int x, int y){
            this.x = x;
            this.y = y;
        }
    }

    public static void main(String[] args){
        List<Point> list = new ArrayList<>();
        list.add(new Point(1, 3));
        list.add(new Point(-1, 6));
        list.add(new Point(4, 7));

        Collections.sort(list, new Comparator<Point>() {
            @Override
            public int compare(Point p1, Point p2){
                return p1.x - p2.x; // 按x递增
            }
        });

        for(Point p:list){
            System.out.println(p.x+" "+p.y);
        }
    }

}
```
另一种方法
```java
import java.util.*;

public class TT1{
    static class Point implements Comparable{
        public int x;
        public int y;
        public Point(int x, int y){
            this.x = x;
            this.y = y;
        }

        @Override
        public int compareTo(Object o){
            Point p = (Point)o;
            return this.x-p.x;
        }
    }

    public static void main(String[] args){
        List<Point> list = new ArrayList<>();
        list.add(new Point(1, 3));
        list.add(new Point(-1, 6));
        list.add(new Point(4, 7));

        Collections.sort(list);

        for(Point p:list){
            System.out.println(p.x+" "+p.y);
        }
    }

}
```

输出：

    -1 6
    1 3
    4 7