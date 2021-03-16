# 计算机网络

## 多播，组播，广播

[参考文章](https://www.cnblogs.com/CNHK1949/p/10680651.html)

单播：点对点通信
多播：一对多
广播：一对所有,问题：广播风暴

## 长连接和短连接

[参考文章](https://www.cnblogs.com/gotodsp/p/6366163.html)

定义？
区别？
何时使用？优缺点？

## 为什么TCP需要3次握手

[参考解答](https://blog.csdn.net/lengxiao1993/article/details/82771768)

## `GET`和`POST`请求的区别

[GET 和 POST 到底有什么区别？ - 杨光的回答 - 知乎](https://www.zhihu.com/question/28586791/answer/145424285)

标准答案:

- GET在浏览器回退时是无害的，而POST会再次提交请求。
- GET产生的URL地址可以被Bookmark，而POST不可以。
- GET请求会被浏览器主动cache，而POST不会，除非手动设置。
- GET请求只能进行url编码，而POST支持多种编码方式。
- GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
- GET请求在URL中传送的参数是有长度限制的，而POST没有。
- 对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
- GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
- GET参数通过URL传递，POST放在Request body中。

2021-3-4
