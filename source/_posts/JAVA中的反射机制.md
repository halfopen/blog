title: JAVA中的反射机制
author: Halfopen
tags:
  - 反射
  - java基础
categories:
  - java
date: 2017-12-11 22:09:00
---
## 类的加载机制

- 装载：通过类的全限定名获取二进制字节流（二进制的class文件），将二进制字节流转换成方法区中的运行时数据结构，在内存中生成Java.lang.class对象。这个时候该类型没有被分配内存，设置默认值，也没有初始化。

- 链接：执行下面的校验、准备和解析步骤，其中解析步骤是可以选择的；

	- 校验：检查导入类或接口的二进制数据的正确性；（文件格式验证，元数据验证，字节码验证，符号引用验证）

	- 准备：给类的静态变量分配并初始化存储空间；

	- 解析：将常量池中的符号引用转成直接引用；

- 初始化：激活类的静态变量的初始化Java代码和静态Java代码块，并初始化程序员设置的变量值。

## 反射机制获取类有三种方法

```java
//第一种方式：  
Class c1 = Class.forName("Employee");  
//第二种方式：  
//java中每个类型都有class 属性.  
Class c2 = Employee.class;  
   
//第三种方式：  
//java语言中任何一个java对象都有getClass 方法  
Employee e = new Employee();  
Class c3 = e.getClass(); //c3是运行时类 (e的运行时类是Employee) 

```

## java中Class.forName和classLoader的区别
java中class.forName和classLoader都可用来对类进行加载。前者除了将类的.class文件加载到jvm中之外，还会对类进行解释，执行类中的static块。

而classLoader只干一件事情，就是将.class文件加载到jvm中，不会执行static中的内容,只有在newInstance才会去执行static块。Class.forName(name, initialize, loader)带参函数也可控制是否加载static块。并且只有调用了newInstance()方法采用调用构造函数，创建类的对象 



```java
class Test{
    static{
        System.out.println("static block");
    }
}

public class Reflect extends ClassLoader{

    public static void main(String[] args) {
        try {
            System.out.println("Class.forName false");
            Class.forName("Test", false, new Reflect());
            System.out.println("Class.forName true");
            Class.forName("Test");

            System.out.println("ClassLoader.loadClass false");
            new Reflect().loadClass("Test");
            System.out.println("ClassLoader.loadClass true");
            new Reflect().loadClass("Test", true);
        } catch (ClassNotFoundException e) {
            e.printStackTrace();
        }

    }
}
```
输出结果

    Class.forName false
    Class.forName true
    static block
    ClassLoader.loadClass false
    ClassLoader.loadClass true

## 总结
Class.forName可以选择是否初始化，默认为初始化，可以自己选择classLoader

classLoader不能初始化，只能选择是否进行链接，默认不链接。自己本身作为classLoader

参考：

http://blog.csdn.net/liujiahan629629/article/details/18013523

http://blog.csdn.net/u011202334/article/details/51497998

https://www.cnblogs.com/clarke157/p/6651195.html