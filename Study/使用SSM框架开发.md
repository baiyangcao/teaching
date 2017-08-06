## 使用 SSM 框架开发手机 APP 发布系统

### 添加验证 @Valid 之后启动 Tomcat 报错

在 `addUser` 方法第一个参数 `User` 前添加注解 `@Valid`之后，
启动 tomcat 服务器部署项目时报错

```shell
org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'org.springframework.validation.beanvalidation.OptionalValidatorFactoryBean#0': Invocation of init method failed; nested exception is java.lang.NoClassDefFoundError: com/fasterxml/classmate/TypeResolver
```

可以看出来报错异常 `NoClassDefFoundError` 找不到类定义错误，
经查后发现，缺少 `classmate.jar` 类库，这是因为在引用 `hibernate-validator.jar` 库时，
没有将其必须的依赖库引用到项目中导致。