# 文件部署
当我们要编写一个Java Web项目时，我们将类编译后需要将项目移到Tomcat的webapps目录下。但是服务器对于文件的放置地点有明确的规定，如图所示：以下是各种文件放置的位置:  

* 部署描述文件web.xml文件必须直接放置在webapps/MyWebProject/WEB_INF/的目录下

* 经过编译的servlet文件格式为.class 文件必须放置在webapps/MyWebProject/WEB_INF/classes/文件目录下

* 导入的相关的第三方库为.jar格式的文件必须放置在webapps/MyWebProject/WEB_INF/lib/目录下

* .tag类型的文件必须放置在webapps/MyWebProject/WEB_INF/tags目录或者其子目录下
[file placement]:


