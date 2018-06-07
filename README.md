# Servlet-JSP

## 如何创建一个Http Servlet
如果我们想要创建一个HttP servlet，那么我们需要做的就是继承 HttpServlet。并且重写其中的doGet、doPost、doPut、doDelete、init、destroy等方法。
## HttPServlet、GenericServlet、Servlet之间的关系
HttPServlet 继承GenericServlet,其中GenericServlet是一个抽象类;GenericServlet实现了Servlet接口和ServletConfig接口;  
|方法|方法描述|
|----|----|
|init(ServletConfig cofig)|容器在第一次请求或者是配置了Tomcat启动时初始化调用该方法|
|service(ServletRequest req,Servlet res)|当请求到来时会将Request和Response传递给service方法，然后根据HTTP请求行中的方法确认调用方法|
|getServletConfig()|如果我们在web.xml配置了初始化参数，那么此方法返回的ServletConfig就会包含设置的参数名-参数值|



## Http请求和web.xml配置文件
Http请求  
GET http://localhost:8080/Web_Example/hello HTTP/1.1  
Host: localhost:8080  
Connection: keep-alive  
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/65.0.3325.146 Safari/537.36  
Accept-Encoding: gzip, deflate, br  
Accept-Language: zh-CN,zh;q=0.9  
我们来看第一行，称之为请求行 分为四个部分。当前主要分析请求行  
传输方案：https表示应用层传输方案是采用HTTP协议  
主机名：www.baidu.com这是一个域名，当客户端发出请求时，会首先由DNS服务器将域名进行解析转成IP地址    
文件路径：/Web_Example/hello 就是文件所在的  
协议版本：HTTP/1.1 表示协议使用的版本  
web.xml  
如何根据Http请求找到相应的对应的Servlet处理请求并做出反应  
第一步：首先根据request 中的文件路径/Web_Example/hello去<servlet-mapping>中的找到与之对应的<url-pattern>为/hello.  
第二步：根据<servlet-mapping>中的<url-pattern> /hello找到对应的对应的<servlet-name>为HelloServlet  
第二步，由第一步的得到<servlet-name>HelloServlet然后去<Servlet>中的找到对应当前<servlet-name>的<servlet-class>为example1.HelloServlet，因此将请求交给HelloServlet处理。  
  
## Servlet的生命周期
用户第一次当前Servlet时，Tomcat容器会调用init()方法(init()方法会调用init(ServletConfig))初始化Servlet;init()方法只调用一次

接着Tomcat创建一个新的线程，并生成相应的HttpServletRequest和HttpServletResponse实例对象并调用service(HttpServletRequest req,HttpServletResponse res)  

service方法根据request获取的请求方法调用service中的doGet\doPost\doDelete\doHead方法
HelloServlet实例
```Java
package example1;

import java.io.IOException;
import java.io.PrintWriter;

import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;

public class HelloServlet extends HttpServlet{
	
	private static final long serialVersionUID = 6549328204442040137L;
	
	private int time =0;//用于记录Servlet请求的次数
	
	public void doGet(HttpServletRequest request,HttpServletResponse response) throws IOException {
		PrintWriter out = response.getWriter();
		getServletConfig().getInitParameterNames();
		
	}
	public void init() {
		System.out.println("Initialize HelloServlet call init() method");
	}
	public void service(HttpServletRequest request,HttpServletResponse response) {
		time ++;
		System.out.println("call service() method times: "+ time);
	}
	public void destory() {
		System.out.println("Close the Servlet");
	}
}
```
web.xml配置文件
```Java
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
		 xmlns="http://java.sun.com/xml/ns/javaee" 
		 xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" 
		 version="2.5">
  <servlet>
  	<servlet-name>HelloServlet</servlet-name>
  	<servlet-class>example1.HelloServlet</servlet-class>
  </servlet> 
  <servlet-mapping>
  	<servlet-name>HelloServlet</servlet-name>
  	<url-pattern>/hello</url-pattern>
  </servlet-mapping>
</web-app>
```
在地址栏中输入http://localhost:8080/Web_Example/hello
显示的结果
```Java
Initialize HelloServlet call init() method
call service() method times: 1
call service() method times: 2
call service() method times: 3
call service() method times: 4
call service() method times: 5
```
从上面的结果可以看到当第一次访问的时候就会调用init(),当刷新网页的时候每次都会调用service()，但并不是每次都会调用init()方法

## Get和Post方法区别
当我们提交表单需要修改后台数据时采用Post方法，Get方法主要是用于提交请求浏览网页  
Get的请求的参数在请求行中，而Post方法提交的请求参数在消息体中  
Get方法的URL限制条件为2048个字符，而Post方法无限制条件  
Get方法是幂等的，而Post方法是非幂等的  

## ServletContext、ServletConfig(web.xml配置方法，所述范围，线程安全性，何时被创建)

## 监听器和过滤器
