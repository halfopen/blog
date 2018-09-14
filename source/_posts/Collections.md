title: Collections
author: Halfopen
tags:
  - java基础
categories:
  - java
date: 2018-03-24 21:46:00
---
[官网api](https://docs.oracle.com/javase/7/docs/api/java/util/Collections.html)

Collections是一个非常实用的工具类，这里了解一下官网api里的方法 

### sort 实现对List类型的排序操作
```java
public static <T> void sort(List<T> list, Comparator<? super T> c)
```


##### 参数
- list - 要排序的list
- c - 可选 比较器，可以自定义比较方法

##### 例子
```java
	Collections.sort(list, new Comparator<Point>(){
    	@Override
        public int compareTo(Point p1, Point p2){
        	return p1.x - p2.x;
        }
    })
```

### binarySearch 二分查找
```java
public static <T> int binarySearch(List<? extends T> list,
                   T key,
                   Comparator<? super T> c)
```
##### 参数
- list - the list to be searched.
- key - the key to be searched for.
- c - the comparator by which the list is ordered. A null value indicates that the elements' natural ordering should be used.

##### 返回
如果找到，返回从0开始的下标>=0，否则返回 -(insertion point)-1

#### reverse 翻转list
```java
public static void reverse(List<?> list)
```


#### shuffle
```java
public static void shuffle(List<?> list, Random rnd))
```
#### swap 交换下标对应元素
```java
public static void swap(List<?> list, int i, int j)
```

#### fill 把list全部修改成同一个值
```java
public static <T> void fill(List<? super T> list,T obj)
```

#### copy 
```java
public static <T> void copy(List<? super T> dest, List<? extends T> src)
```
#### min&max
```java
public static <T extends Object & Comparable<? super T>> T min(Collection<? extends T> coll)
```

#### rotate
```java
public static void rotate(List<?> list, int distance)
```

#### replaceAll
```java
public static <T> boolean replaceAll(List<T> list,
                     T oldVal,
                     T newVal)
```

#### indexOfSubList lastIndexOfSubList
```java
public static int indexOfSubList(List<?> source,
                 List<?> target)
```
                 
#### singleton
```java
public static <T> Set<T> singleton(T o)
```
返回一个不可变的集合只包含指定对象。

一般可以配合removeAll使用，因为removeAll接受的参数是Set
##### 例子
```java
import java.util.*;

public class CollectionsDemo {
   public static void main(String args[]) {
      // create an array of string objs
      String init[] = { "One", "Two", "Three", "One", "Two", "Three" };
      
      // create two lists
      List list1 = new ArrayList(Arrays.asList(init));
      List list2 = new ArrayList(Arrays.asList(init));
      
      // remove from list1
      list1.remove("One");
      System.out.println("List1 value: "+list1);
      
      // remove from list2 using singleton
      list2.removeAll(Collections.singleton("One"));		   
      System.out.println("The SingletonList is :"+list2);
   }
}
```

    List1 value: [Two, Three, One, Two, Three]
    The SingletonList is :[Two, Three, Two, Three]
    
# 优先队列

