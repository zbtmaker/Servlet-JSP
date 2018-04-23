# Request 方法
## HTTP协议参数
  Servlet的请求参数以字符串的形式作为请求的一部分发送到Servlet容器，当请求是一个HttpServletRequest时，容器会从URI查询字符串(GET方法)或请求体中（POST方法）填充参数。这里为什么是两种呢？当我们的请求方法为GET时，我们的参数是在URI中，当我们的请求方法是POST时。我们的请求方法在请求体中:
* 当我们的请求方法设置为GET时
```Java
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>beer selection</title>
</head>
<body>
<h1 algin="center">Beer Selection Page</h1>
<form method="GET" action="Selection.do">
	Selection beer characteristics<p>
	Color:
	<select name="color" size=1>
		<option value="light"> light</option>
		<option value="amber"> amber</option>
		<option value="brown">brown</option>
		<option value="dark">dark</option>
	</select>
	<br><br>
	<center>
		<input type="submit" value="submit">
	</center>
</form>
</body>
</html>
```
我们看看我们的请求信息,参数在URI的"?"后面就是我们的参数color=light
```Java
GET http://localhost:8080/Beer_v1/Selection.do?color=light HTTP/1.1
Accept: text/html, application/xhtml+xml, image/jxr, */*
Referer: http://localhost:8080/Beer_v1/form.html
Accept-Language: zh-CN
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299
Accept-Encoding: gzip, deflate
Host: localhost:8080
Connection: Keep-Alive
Cookie: JSESSIONID=ACCFF0F37B71C973D732059E3075F238
```
* 当我们在表单中的请求方法设置为"POST"时，如下：
```Java
<form method="GET" action="Selection.do">
```
我们从请求消息中可以看到如下：
```Java
POST http://localhost:8080/Beer_v1/Selection.do HTTP/1.1
Accept: text/html, application/xhtml+xml, image/jxr, */*
Referer: http://localhost:8080/Beer_v1/
Accept-Language: zh-CN
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/58.0.3029.110 Safari/537.36 Edge/16.16299
Content-Type: application/x-www-form-urlencoded
Accept-Encoding: gzip, deflate
Content-Length: 11
Host: localhost:8080
Connection: Keep-Alive
Pragma: no-cache
Cookie: JSESSIONID=ACCFF0F37B71C973D732059E3075F238

color=light
```
从上面我们可以看到请求参数并不在URI中，而是在请求体中。
* HttPServletRequest 中获取参数的几种方法
  * String getParameter(String name)
    我们如果想要获得color这个参数的value，那么我们我们就需要执行下面的语句：
    ```Java
    String c = request.getParameter("color");
    ```
    此时String c = "light";
  * Enumeration getParameterNames()
  * String[] getParameterValues()
  *

