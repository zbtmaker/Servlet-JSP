# Servlet-JSP

## 如何创建一个Http Servlet
如果我们想要创建一个HttP servlet，那么我们需要做的就是继承 HttpServlet。并且重写其中的doGet、doPost、doPut、doDelete、init、destroy等方法。
## HttPServlet、GenericServlet、Servlet之间的关系
HttPServlet 继承GenericServlet,其中GenericServlet是一个抽象类;GenericServlet实现了Servlet接口和ServletConfig接口;
## Http请求和web.xml配置文件
## Servlet的生命周期
用户第一次当前Servlet时，Tomcat容器会调用init()方法(init()方法会调用init(ServletConfig))初始化Servlet;init()方法只调用一次  
接着Tomcat创建一个新的线程，并生成相应的HttpServletRequest和HttpServletResponse实例对象并调用service(HttpServletRequest req,HttpServletResponse res)  
service方法根据request获取的请求方法调用service中的doGet\doPost\doDelete\doHead方法
## Get和Post方法区别
## ServletContext、ServletConfig(web.xml配置方法，所述范围，线程安全性，何时被创建)
## 监听器和过滤器
