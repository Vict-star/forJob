# java注解

参考来源

- [菜鸟：Java 注解（Annotation）](https://www.runoob.com/w3cnote/java-annotation.html)
- [简书：Java 注解完全解析](https://www.jianshu.com/p/9471d6bcf4cf)

## 官方文档

java注解用于为java代码提供元数据。作为元数据，注解不会直接影响代码运行，但也有一些类型的注解实际上可以用于这一目的。

## 注解的定义

一种类的类型

## 注解类的写法

```java
public @interface MyTestAnnotation {
}//MyTestAnnotation即为注解类

@MyTestAnnotation
public class test {
   @MyTestAnnotation
   public static void main(String[] args){
   }
}
```

## 元注解

注解的注解，作用于注解，方便为创建的注解实现想要的功能。  
分别有`@Retention`,`@Target`,`@Document`,`@Inherited`和`@Repeatable`(java1.8加入)五种。

### `@Retention`

Retention英文意思有保留、保持的意思，它表示注解存在阶段是保留在源码（编译期），字节码（类加载）或者运行期（JVM中运行）。在@Retention注解中使用枚举RetentionPolicy来表示注解保留时期

1. @Retention(RetentionPolicy.SOURCE)，注解仅存在于源码中，在class字节码文件中不包含
2. @Retention(RetentionPolicy.CLASS)， 默认的保留策略，注解会在class字节码文件中存在，但运行时无法获得
3. @Retention(RetentionPolicy.RUNTIME)， 注解会在class字节码文件中存在，在运行时可以通过反射获取到

如果我们是自定义注解，则通过前面分析，我们自定义注解如果只存着源码中或者字节码文件中就无法发挥作用，而在运行期间能获取到注解才能实现我们目的，所以自定义注解中肯定是使用 @Retention(RetentionPolicy.RUNTIME)

### `@Target`

限制自定义注解作用的范围:

- @Target(ElementType.TYPE) 作用接口、类、枚举、注解
- @Target(ElementType.FIELD) 作用属性字段、枚举的常量
- @Target(ElementType.METHOD) 作用方法
- @Target(ElementType.PARAMETER) 作用方法参数
- @Target(ElementType.CONSTRUCTOR) 作用构造函数
- @Target(ElementType.LOCAL_VARIABLE)作用局部变量
- @Target(ElementType.ANNOTATION_TYPE)作用于注解（@Retention注解中就使用该属性）
- @Target(ElementType.PACKAGE) 作用于包
- @Target(ElementType.TYPE_PARAMETER) 作用于类型泛型，即泛型方法、泛型类、泛型接口 （jdk1.8加入）
- @Target(ElementType.TYPE_USE) 类型使用.可以用于标注任意类型除了 class （jdk1.8加入）

常用`Element.type`类型

### `@Document`

将注解中的元素包含到JavaDoc中。

### `@Inherited`

一个被@Inherited注解了的注解修饰了一个父类，如果他的子类没有被其他注解修饰，则它的子类也继承了父类的注解。

例子：

```java
/**自定义注解*/
@Documented
@Inherited
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MyTestAnnotation {
}
/**父类标注自定义注解*/
@MyTestAnnotation
public class Father {
}
/**子类*/
public class Son extends Father {
}
/**测试子类获取父类自定义注解*/
public class test {
   public static void main(String[] args){

      //获取Son的class对象
       Class<Son> sonClass = Son.class;
      // 获取Son类上的注解MyTestAnnotation可以执行成功
      MyTestAnnotation annotation = sonClass.getAnnotation(MyTestAnnotation.class);
   }
}
```

### `@Repeatable`(Javv8开始支持)

标识某注解可以在同一声明下使用多次。

## 注解的本质

注解的本质就是一个Annotation接口

## 注解属性类型

注解属性类型可以有以下列出的类型

1. 基本数据类型
2. String
3. 枚举类型
4. 注解类型
5. Class类型
6. 以上类型的一维数组类型

## 注解成员变量赋值

如果注解又多个属性，则可以在注解括号中用“，”号隔开分别给对应的属性赋值，如下例子，注解在父类中赋值属性

```java
@Documented
@Inherited
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface MyTestAnnotation {
    String name() default "mao";
    int age() default 18;
}

@MyTestAnnotation(name = "father",age = 50)
public class Father {
}
```

## 获取注解属性

使用Java的反射：

通过`isAnnotationPresent`判断是否存在某个注解，通过`getAnnotation`获取注解对象，然后获取值

## JDK内置的注解类型

![alt Annotation架构](annotation.jpg)

### 内置的注解

Java 定义了一套注解，共有 7 个，3 个在 java.lang 中，剩下 4 个在 java.lang.annotation 中。

#### 作用在代码的注解是

- @Override - 检查该方法是否是重写方法。如果发现其父类，或者是引用的接口中并没有该方法时，会报编译错误。
- @Deprecated - 标记过时方法。如果使用该方法，会报编译警告。
- @SuppressWarnings - 指示编译器去忽略注解中声明的警告。

#### 作用在其他注解的注解(或者说 元注解)是

- @Retention - 标识这个注解怎么保存，是只在代码中，还是编入class文件中，或者是在运行时可以通过反射访问。
- @Documented - 标记这些注解是否包含在用户文档中。
- @Target - 标记这个注解应该是哪种 Java 成员。
- @Inherited - 标记这个注解是继承于哪个注解类(默认 注解并没有继承于任何子类)

#### 从 Java 7 开始，额外添加了 3 个注解

- @SafeVarargs - Java 7 开始支持，忽略任何使用参数为泛型变量的方法或构造函数调用产生的警告。
- @FunctionalInterface - Java 8 开始支持，标识一个匿名函数或函数式接口。
- @Repeatable - Java 8 开始支持，标识某注解可以在同一个声明上使用多次。

## 注解的作用与应用

1. 使用注解进行参数配置  
例子：假设银行有个转账业务，转账的限额可能会根据汇率的变化而变化，我们可以利用注解灵活配置转账的限额，而不用每次都去修改我们的业务代码。  
只要汇率变化，我们就改变注解的配置值就可以直接改变当前最大限额。

2. 第三方框架的应用，如`springboot`、`Junit`等

作用：

- 提供信息给编译器： 编译器可以利用注解来检测出错误或者警告信息，打印出日志。
- 编译阶段时的处理： 软件工具可以用来利用注解信息来自动生成代码、文档或者做其它相应的自动处理。
- 运行时处理： 某些注解可以在程序运行的时候接受代码的提取，自动做相应的操作。
- 正如官方文档的那句话所说，注解能够提供元数据，转账例子中处理获取注解值的过程是我们开发者直接写的注解提取逻辑，处理提取和处理 Annotation 的代码统称为 APT（Annotation Processing Tool)。上面转账例子中的processAnnotationMoney方法就可以理解为APT工具类。
