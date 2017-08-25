---
title: Struts中文问题的解决
date: '2005-08-03'
description:
categories:
- 技术
tags:

---

struts的中文乱码问题主要存在3个地方：
 
###### jsp页面

设置<%@ page contentType="text/html;charset=UTF-8" %>。
 
###### request对象

中文数据在经过struts处理过的request后会有乱码问题。这个问题有几种解决方法，最简单的是从ActionServlet中继承一个MyActionServlet类，代码如下：
 
	public class MyActionServlet extends ActionServlet {
	  protected void process(HttpServletRequest request,
	            HttpServletResponse response) throws java.io.IOException,
	            javax.servlet.ServletException {
	    request.setCharacterEncoding("UTF-8");
	    super.process(request, response);
	  }
	}

别忘了在web.xml中设置，内容如下：

	<servlet>
      <servlet-name>action</servlet-name>
      <servlet-class>com.shu.imrdes.global.MyActionServlet</servlet-class>
      <init-param>
         <param-name>config</param-name>
         <param-value>/WEB-INF/struts-config.xml</param-value>
      </init-param>
      <init-param>
         <param-name>debug</param-name>
         <param-value>3</param-value>
      </init-param>
      <init-param>
         <param-name>detail</param-name>
         <param-value>3</param-value>
      </init-param>
      <load-on-startup>0</load-on-startup>
	</servlet>
	<servlet-mapping>
      <servlet-name>action</servlet-name>
      <url-pattern>*.do</url-pattern>
	</servlet-mapping>
 
###### URL

在URL中传递中文会在编码过程中出现乱码。解决方法如下:

在Tomcat的server.xml中的Connector元素中添加属性URIEncoding="UTF-8"。