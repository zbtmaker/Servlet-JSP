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
http://localhost:8080/com/example/BeerSelectServlet/Beer/SelectBeer.do
```
```Java
http://localhost:8080/com/example/BeerSelectServlet/Beer/SelectBeer
```
我们容器就会根据映射文件的输出界面都是返回com/example/BeerSelectServlet所呈现的内容

## 4 根据URL查找对应Servlet
当我们从浏览器输入一个URL时，我们的配置文件需要根据URL找到我们的servlet执行，下面是三种查找方式：
* 完全匹配:当我们的URL和我们的配置文件中某一个servlet的映射的url-pattern一模一样时.完全匹配时url-pattern的属性以/开头，可以有扩展名
```Java
<servlet>
  <servlet-name>Beer</servlet-name>
  <servlet-class>com.example.BeerSelectServlet</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>Beer</servlet-name>
  <url-pattern>/Beer/SelectBeer</url-pattern>
</servlet-mapping>
```
此时输入的URL为：
```Java
http://localhost:8080/com/example/BeerSelectServlet/Beer/SelectBeer
```

* 目录匹配:url-pattern中的属性以/开头，以`*`结尾
```Java
<servlet>
  <servlet-name>Beer</servlet-name>
  <servlet-class>com.example.BeerSelectServlet</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>Beer</servlet-name>
  <url-pattern>/Beer/`*`</url-pattern>
</servlet-mapping>
```
此时输入的URL为:
```Java
http://localhost:8080/com/example/BeerSelectServlet/Beer/SelectBeer
```
我们的Beer/SelectBeer与url-pattern中的/Beer相匹配，然后发现SelectBeer没有完全匹配的url-pattern,因此就只能与这个进行相匹配

* 扩展名匹配：以`*`开头，以扩展名结尾。首先我们的url会通过完全匹配的方式进行匹配，发现完全匹配不成功后，采用目录匹配的方式继续与servlet当中的url-pattern进行匹配，当目录匹配也失败后，则采用扩展名进行匹配。最后如果扩展名也匹配失败，那么我们就需要返回一个404状态码
```Java
<servlet>
  <servlet-name>Beer</servlet-name>
  <servlet-class>com.example.BeerSelectServlet</servlet-class>
</servlet>
<servlet-mapping>
  <servlet-name>Beer</servlet-name>
  <url-pattern>*.do</url-pattern>
</servlet-mapping>
```
此时输入的URL为：
```Java
http://localhost:8080/com/example/BeerSelectServlet/Beer/SelectBeer.do
```


