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

### IDEA 中 Servlet 的配置

Servlet 在读取的过程中会到 `WEB-INF/classes` 文件夹下去寻找相应的 `.class` 文件，但是默认 IDEA 并不会在 `WEB-INF` 目录下创建 `classes` 目录并将 `.java` 文件编译生成到这个目录，一般情况下会将 `.java` 文件编译生成到 `out/production` 目录下，所以在运行的时候会出现 `HTTP 404` 错误，此时需要做如下配置：

1. 在 `WEB-INF` 目录下创建 `classes` 目录
2. `File` - `Project Structure`， 在弹出的 `Project Structure` 对话框中选择当前模块，并在 `Path` 标签页中设置 `Complier output` 为 `Use module compile output path`，然后将 `Output path` 和 `Test output path` 设置为上一步创建的 `WEB-INF/classes` 目录即可

### JSTL: According to TLD or attribute directive in tag file, attribute value does not accept any expressions

在使用 JSTL 过程执行如下代码：

```jsp
<c:out value="${msg}" default="null" />
```

报错如下：

```
According to TLD or attribute directive in tag file, attribute value does not accept any expressions
```

解决办法：

```jsp
// <%@ taglib uri="http://java.sun.com/jsp/jstl/core" prefix="c" %>
// 将上述标签换成如下标签
<%@ taglib uri="http://java.sun.com/jstl/core" prefix="c" %>
```
