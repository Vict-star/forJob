# Q&A springboot

## Springboot和SpringMVC的关系

[参考文章](https://www.php.cn/java/base/462210.html)

## AOP相关

### AOP的使用

[参考文章](https://blog.csdn.net/qq_33257527/article/details/82561635)

使用方式：直接使用(配置Pointcut匹配方法)，自定义注解(在需要使用到切面的地方标注注解)

- `@Aspect` 表明是一个切面类
- `@Component` 将当前类注入到Spring容器内
- `@Pointcut` 切入点，其中execution用于使用切面的连接点。使用方法：execution(方法修饰符(可选) 返回类型 方法名 参数 异常模式(可选)) ，可以使用通配符匹配字符，*可以匹配任意字符。
- `@Before` 在方法前执行
- `@After` 在方法后执行
- `@AfterReturning` 在方法执行后返回一个结果后执行
- `@AfterThrowing` 在方法执行过程中抛出异常的时候执行
- `@Around` 环绕通知，就是可以在执行前后都使用，这个方法参数必须为ProceedingJoinPoint，proceed()方法就是被切面的方法，上面四个方法可以使用JoinPoint，JoinPoint包含了类名，被切面的方法名，参数等信息。

### AOP源码实现

[Springboot AOP源码讲解](https://www.bilibili.com/video/BV1LA411J7nE?p=4&spm_id_from=pageDriver)

[SpringBoot2 | Spring AOP 原理深度源码分析（八）](https://blog.csdn.net/woshilijiuyi/article/details/83934407)

### java动态代理？

### springboot的启动流程 & Bean的生命周期

[SpringBoot启动流程解析](https://www.cnblogs.com/trgl/p/7353782.html)

![alt springboot启动流程](springboot启动流程.png)

[Bean的生命周期](https://www.cnblogs.com/zrtqsk/p/3735273.html)

[SpringBoot2 | SpringBoot启动流程源码分析（一）](https://blog.csdn.net/woshilijiuyi/article/details/82219585)

## jwt验证相关

[Springboot使用jwt](https://www.jianshu.com/p/e88d3f8151db)

[参考文章](https://www.jianshu.com/p/f111328ea8c4)

## Springboot生命周期

[参考文章](https://blog.csdn.net/qq_42714869/article/details/90378124)

1、初始化环境变量
2、初始化环境变量完成

3、应用启动
4、应用已启动完成

5、应用刷新
6、应用停止
7、应用关闭

## Spring容器初始化过程

[参考文章](https://blog.csdn.net/qq_39632561/article/details/83070140)

1、 初始化过程：
Spring 启动时读取应用程序提供的Bean配置信息，并在Spring容器中生成一份相应的Bean配置注册表，然后根据这张注册表实例化Bean，装配好Bean之间的依赖关系，为上层应用提供准备就绪的运行环境

2、Bean的初始化过程
