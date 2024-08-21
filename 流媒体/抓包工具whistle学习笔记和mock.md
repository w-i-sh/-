whistle

[官方说明文档](https://wproxy.org/whistle/)




主要用于查看、修改HTTP、HTTPS、Websocket的请求、响应，不同于Fiddler通过断点修改请求响应的方式，whistle采用的是类似配置系统hosts的方式，一切操作都可以通过配置实现，支持域名、路径、正则表达式、通配符、通配路径等多种匹配方式




### 安装：

1.下载node.js

2.安装whistle

3.启动while

4.配置代理（浏览器代理记得开）

5.安装代理




简单使用：

__跳转百度抓包__

![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image.png?raw=true)

__使用rules来解析域名__

将www.baidu.com的域名匹配到0.0.0.0

![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy.png?raw=true)
![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%202.png?raw=true)

__mock响应__

可以右键快捷添加也可以下载到本地再引用
![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%203.png?raw=true)

但是直接引用的话好像无法直接定义json文件的名称，而是直接使用的文件的哈希值来命名，目前没找到直接命名的方法

本地引用把{xxx}变成本地文件地址就好




__修改请求__

将百度请求修改为b站
![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%204.png?raw=true)
![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%205.png?raw=true)


设置delay和speed

时延和速度

![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%206.png?raw=true)

设置成功后明显感觉响应有了时间间隔，请求的速度变得很慢




statuscode设置响应码

![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%207.png?raw=true)
![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%208.png?raw=true)








查看log

![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%209.png?raw=true)
![图片](https://github.com/w-i-sh/blog-img/blob/main/%E6%B5%81%E5%AA%92%E4%BD%93/image%20copy%2010.png?raw=true)


__wireshark__

安装exe

选择对应的网卡来进行抓包







### mock

在这里记录一下mock是什么

mock是用来模拟服务器响应的一种工具

mock的使用场景

1、前后端的分离，解决前后端依赖

2、解决外部接口依赖或者外部接口的异常的接口场景测试

3、来进行产品演示


