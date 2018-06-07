# Servlet-JSP

## 如何创建一个Http Servlet
如果我们想要创建一个HTTP servlet，那么我们需要做的就是继承 HttpServlet。并且重写其中的doGet、doPOST、doPut、doDelete、init、destroy等方法。
## HttPServlet、GenericServlet、Servlet之间的关系
HttPServlet 继承GenericServlet,其中GenericServlet是一个抽象类;GenericServlet实现了Servlet接口和ServletConfig接口;

## Servlet的生命周期
## Http请求和web.xml配置文件
## Get和Post方法区别
## ServletContext、ServletConfig(web.xml配置方法，所述范围，线程安全性，何时被创建)
## 监听器和过滤器
