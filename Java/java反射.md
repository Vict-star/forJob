- [什么是反射,java反射的三种实现方式](#什么是反射java反射的三种实现方式)
  - [第一种表示方式](#第一种表示方式)
  - [第二种表达方式：已经知道该类的对象通过getClass方法](#第二种表达方式已经知道该类的对象通过getclass方法)
  - [第三种表示方式](#第三种表示方式)
  
# 什么是反射,java反射的三种实现方式
Java的反射（reflection）机制是指在程序的**运行状态中**，可以构造任意一个类的对象，可以了解任意一个对象所属的类，可以了解任意一个类的成员变量和方法，可以调用任意一个对象的属性和方法。这种动态获取程序信息以及动态调用对象的功能称为Java语言的反射机制。反射被视为动态语言的关键。

都以Foo为类名举例
表示实例对象的方式：
类名 表示名=new 类名（）；
//Foo的实例对象如何表示
 ```java
Foo foo1 = new Foo();
```
任何一个类都是Class的实例对象，这个实例对象有三种表示方式：
任何一个类都有一个隐含的静态成员变量class
## 第一种表示方式
```java
Class c1=Foo.class；//注意Class要大写C
```
##  第二种表达方式：已经知道该类的对象通过getClass方法
```java
Class c2 = foo1.getClass();
//c1 ,c2 表示了Foo类的类类型(class type)
```

## 第三种表示方式
```java
Class c3=null;
try
{
    c3=Class.forName("Foo的相对路径");
}
catch (Exception e)
{
    e.printStackTrace();
}
//可以使用newInstance方法创建Foo的实例对象
try
{
    Foo foo=(Foo)c1.newInstance();
//(Foo)Foo是Foo的接口
    foo.print();
}catch (Exception e){e.printStackTrace();
}
/*通过Foo的接口来找到Foo的类类型
*然后通过newInstance()方法来初始化一个类
*生成一个实例对象。
*使用newInstance方法时必须保证：这个类已经加载
*这个类已经连接了。完成这俩步的正是class的静态方法forName（）方法
*这个方法调用了启动类加载器（java api的加载器）*/
```
动态加载类:  

    try{
    Class c=class.forName(args[0]);
    类名 表示名 =（接口）c.newInstance();
    表示名.方法();
    }catch(Exception e){e.printStrckTrace}