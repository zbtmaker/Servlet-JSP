# 文件部署
## 1 文件放置规则
当我们要编写一个Java Web项目时，我们将类编译后需要将项目移到Tomcat的webapps目录下。但是服务器对于文件的放置地点有明确的规定，以下是各种文件放置的位置:  

* 部署描述文件web.xml文件必须直接放置在webapps/MyWebProject/WEB_INF/的目录下

* 经过编译的servlet文件格式为.class 文件必须放置在webapps/MyWebProject/WEB_INF/classes/文件目录下

* 导入的相关的第三方库为.jar格式的文件必须放置在webapps/MyWebProject/WEB_INF/lib/目录下

* .tag类型的文件必须放置在webapps/MyWebProject/WEB_INF/tags目录或者其子目录下

## 2 正确访问方式
WEB-INF/MET-INF下的文件不能通过浏览器直接获取，如果有些内容我们不想让用户直接从浏览器通过路径名获取，那么我们就应该将这些内容放置在这两个文件夹下。一般来说，我们的欢迎文件列表<welcome-file-list></welcome-file-list>都直接放置在WEB-INF文件夹下。  
* 正确访问路径
```Java
http://localhost:8080/examples/index.html
```
* 错误访问路径
```Java
http://localhost:8080/examples/INF/web.xml
```
## 3 Servlet映射和URL匹配
一个servlet映射可以对应多个URL，如下所示：

```Java
<servlet>
  <servlet-name>Beer</servlet-name>
  <servlet-class>com.example.BeerSelectServlet</servlet-class>
</servlet>

<servlet-mapping>
  <servlet-name>Beer</servlet-name>
  <url-pattern>/Beer/SelectBeer.do</url-pattern>
</servlet-mapping>

<servlet-mapping>
  <servlet-name>Beer</servlet-name>
  <url-pattern>/Beer/SelectBeer</url-pattern>
</servlet-mapping>
```
当我们在浏览器中输入下面的URL时：
```Java
http://localhost:8080/com/example/BeerSelectServlet/SelectBeer.do
```
```Java
http://localhost:8080/com/example/BeerSelectServlet/SelectBeer
```
我们的输出界面都是返回com/example/BeerSelectServlet所呈现的内容


