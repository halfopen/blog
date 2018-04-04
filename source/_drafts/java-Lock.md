title: java Lock
author: Halfopen
tags:
  - 并发
  - ''
categories:
  - java
date: 2018-04-02 21:30:00
---
# Lock接口

```java
public interface Lock {

    void lock();

    void lockInterruptibly() throws InterruptedException; //让线程可以响应中断

    boolean tryLock(); //尝试获取锁，如果获取成功，则返回true，如果获取失败（即锁已被其他线程获取），则返回false

    boolean tryLock(long time, TimeUnit unit) throws InterruptedException;

    void unlock();

    Condition newCondition();
}

```
一般使用形式 
```java
Lock lock = ...;
lock.lock();
try{
    //处理任务
}catch(Exception ex){
     
}finally{
    lock.unlock();   //释放锁
}
```
一般情况下通过tryLock来获取锁时是这样使用的
```java
Lock lock = ...;
if(lock.tryLock()) {
     try{
         //处理任务
     }catch(Exception ex){
         
     }finally{
         lock.unlock();   //释放锁
     } 
}else {
    //如果不能获取锁，则直接做其他事情
}
```

Lock接口可以手动释放锁，并且知道是否加锁成功。
但如果不手动释放锁，可能会导致死锁。

## ReentrantLock

我们可以在创建ReentrantLock对象时，通过以下方式来设置锁的公平性：

ReentrantLock lock = new ReentrantLock(true);
 　　如果参数为true表示为公平锁，为fasle为非公平锁。默认情况下，如果使用无参构造器，则是非公平锁。

　　另外在ReentrantLock类中定义了很多方法，比如：

　　isFair()        //判断锁是否是公平锁

　　isLocked()    //判断锁是否被任何线程获取了

　　isHeldByCurrentThread()   //判断锁是否被当前线程获取了

　　hasQueuedThreads()   //判断是否有线程在等待该锁

　　在ReentrantReadWriteLock中也有类似的方法，同样也可以设置为公平锁和非公平锁。不过要记住，ReentrantReadWriteLock并未实现Lock接口，它实现的是ReadWriteLock接口。



## Condition

## ReadWriteLock

## ReentrantReadWriteLock


http://www.cnblogs.com/dolphin0520/p/3923167.html

https://blog.csdn.net/yanyan19880509/article/details/52345422

https://blog.csdn.net/jiangjiajian2008/article/details/52226189

https://blog.csdn.net/antony9118/article/details/52664125