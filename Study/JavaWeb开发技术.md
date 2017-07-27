## Java Web 开发技术与实战项目

### 请求中文乱码的处理

 - 对于 POST 请求，使用 `request.setCharacter("UTF-8")` 设置解码方式为 `UTF-8`

> 注意： 这里发起请求页面的编码也应该为 `UTF-8`
> ```jsp
> <%@ page contentType="text/html;charset=UTF-8" %>
> ```

 - 对于 Get 请求，进行字符串编码转换

```java
String name = request.getParameter("name");
// Tomcat 默认的解码方式为 ISO-8859-1
name = new String(name.getBytes("ISO-8859-1"), "UTF-8");
```

 - 在 Get 请求中，还可以在 Tomcat 中设置字符集

```xml
<Connector port="8080" protocol="HTTP/1.1"
    connectionTimeout="20000"
    redirectPort="8443" URIEncoding="UTF-8" />
```
