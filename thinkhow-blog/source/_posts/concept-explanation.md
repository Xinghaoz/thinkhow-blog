---
title: concept explanation
date: 2016-07-02 22:32:18
tags:
---

什么是前端，什么是后端，什么是框架，什么又是MVC，MVT？java, python, PHP, javascript对应的是哪端的语言？Apache, Tomcat, Nginx, Angular, Django, Express, Node.js又是什么？它们是同一个东西吗？如果不是的话，哪个对应哪个呢？

CC课的Team Project刚开始时，TA扔给我们一个网址说，上面有各个框架的测评情况，你们可以参考一下。用哪个框架你们自己去定。
嗯，这看起来挺不错的。可是。。。神马是框架啊！问了几个同学，很多人也一头雾水，或者了解一点但是没有清楚的认识。

之后，又接触到了Node.js，号称可以用javascript写后端，这样前端人员也可以做后端的事情了。等一下，Node.js是什么？是服务器，还是框架？或者两者都不是？
在建站之前，有很多概念和名词是需要我们区分和理解的。哪个属于前端的东西，哪个属于后端的东西。这个东西横向又有什么可以对比。根据这段时间磕磕绊绊的经历和不断地看文档收集资料，自己也慢慢理清了一些思路。但最好的​理解方法就是去用那个东西，去用Tomcat写个java servlet，去用Node.js写一个博客就会知道这个东西是什么，能干什么用了。

## 前端

各个语言常用的Web框架：
Java: Spring
Python：Django, Flask, Pyramid, tornado
Node.js: Express

## 后端
### 从LAMP技术栈谈起
我的思路就是按照技术栈从上到下列出每一层，简单说明一下每一层的作用。然后每一层再横向展开，列出这一层比较热门的技术。有了这个纵向和横向的对比，相信我们就会对每个东西是什么有一个准确的定位。
LAMP就是:
Linux   - Operating System
Apache  - Web Server
MySQL   - database
PHP     - Backend Language
