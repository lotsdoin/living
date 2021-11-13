# Tomcat 学习

* Tomcat 是什么？
  Tomcat 是 Web 容器，作为网页和后台程序的桥梁。 Java 语言相关 Web 容器一般有 HTTP 服务器和 Servlet 容器
  HTTP 服务器（Apache、Nginx）处理静态页面，向浏览器返回静态 HTML，浏览器负责解析 HTML，将结果呈现给用户。
  JBoss、WebLogic不仅仅有 Servlet 容器的功能，也包含 EJB 容器，是完整的 Java EE 应用服务器。
* HTTP 的本质
  HTTP 协议是浏览器与服务器之间的数据传输协议。作为应用层协议，HTTP 是基于 TCP/IP 协议来传输数据的（HTML文件、图片）
  HTTP 协议不涉及数据包 （Packet） 传输，主要规定了客户端和服务器之间的通信格式。
  