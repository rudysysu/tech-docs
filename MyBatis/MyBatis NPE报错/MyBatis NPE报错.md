
## 程序启动的时候报错
```
2024-05-16 10:49:01,104 [4962467978662539265][Dispatch-Service-thread-15] [ThriftChannelAccessFilter.java:147] [WARN ThriftChannelAccessFilter] - ...... throws:org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: java.lang.NullPointerException
### Cause: java.lang.NullPointerException used:9,delay:0,errorStack:
org.mybatis.spring.MyBatisSystemException: nested exception is org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: java.lang.NullPointerException
### Cause: java.lang.NullPointerException
	at org.mybatis.spring.MyBatisExceptionTranslator.translateExceptionIfPossible(MyBatisExceptionTranslator.java:73)
	at org.mybatis.spring.SqlSessionTemplate$SqlSessionInterceptor.invoke(SqlSessionTemplate.java:364)
	at com.sun.proxy.$Proxy42.selectList(Unknown Source)
	at org.mybatis.spring.SqlSessionTemplate.selectList(SqlSessionTemplate.java:194)
	at org.apache.ibatis.binding.MapperMethod.executeForMany(MapperMethod.java:114)
	at org.apache.ibatis.binding.MapperMethod.execute(MapperMethod.java:58)
	at org.apache.ibatis.binding.MapperProxy.invoke(MapperProxy.java:43)
	at com.sun.proxy.$Proxy137.selectByExample(Unknown Source)
	......
	at org.springframework.cglib.proxy.MethodProxy.invoke(MethodProxy.java:204)
	at org.springframework.aop.framework.CglibAopProxy$CglibMethodInvocation.invokeJoinpoint(CglibAopProxy.java:738)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:157)
	at org.springframework.aop.aspectj.MethodInvocationProceedingJoinPoint.proceed(MethodInvocationProceedingJoinPoint.java:85)
    ......
	at sun.reflect.GeneratedMethodAccessor174.invoke(Unknown Source)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.springframework.aop.aspectj.AbstractAspectJAdvice.invokeAdviceMethodWithGivenArgs(AbstractAspectJAdvice.java:627)
	at org.springframework.aop.aspectj.AbstractAspectJAdvice.invokeAdviceMethod(AbstractAspectJAdvice.java:616)
	at org.springframework.aop.aspectj.AspectJAroundAdvice.invoke(AspectJAroundAdvice.java:70)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:168)
	at org.springframework.aop.interceptor.ExposeInvocationInterceptor.invoke(ExposeInvocationInterceptor.java:92)
	at org.springframework.aop.framework.ReflectiveMethodInvocation.proceed(ReflectiveMethodInvocation.java:179)
	at org.springframework.aop.framework.CglibAopProxy$DynamicAdvisedInterceptor.intercept(CglibAopProxy.java:673)
	......
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
    ......
	at java.util.concurrent.ThreadPoolExecutor.runWorker(ThreadPoolExecutor.java:1149)
	at java.util.concurrent.ThreadPoolExecutor$Worker.run(ThreadPoolExecutor.java:624)
	at java.lang.Thread.run(Thread.java:748)
Caused by: org.apache.ibatis.exceptions.PersistenceException: 
### Error querying database.  Cause: java.lang.NullPointerException
### Cause: java.lang.NullPointerException
	at org.apache.ibatis.exceptions.ExceptionFactory.wrapException(ExceptionFactory.java:23)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:107)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:98)
	at sun.reflect.NativeMethodAccessorImpl.invoke0(Native Method)
	at sun.reflect.NativeMethodAccessorImpl.invoke(NativeMethodAccessorImpl.java:62)
	at sun.reflect.DelegatingMethodAccessorImpl.invoke(DelegatingMethodAccessorImpl.java:43)
	at java.lang.reflect.Method.invoke(Method.java:498)
	at org.mybatis.spring.SqlSessionTemplate$SqlSessionInterceptor.invoke(SqlSessionTemplate.java:354)
	... 43 common frames omitted
Caused by: java.lang.NullPointerException: null
	at org.apache.ibatis.reflection.property.PropertyTokenizer.<init>(PropertyTokenizer.java:27)
	at org.apache.ibatis.reflection.MetaObject.getValue(MetaObject.java:104)
	at org.apache.ibatis.scripting.xmltags.DynamicContext$ContextMap.get(DynamicContext.java:89)
	at org.apache.ibatis.scripting.xmltags.DynamicContext$ContextAccessor.getProperty(DynamicContext.java:107)
	at org.apache.ibatis.ognl.OgnlRuntime.getProperty(OgnlRuntime.java:1657)
	at org.apache.ibatis.ognl.ASTProperty.getValueBody(ASTProperty.java:92)
	at org.apache.ibatis.ognl.SimpleNode.evaluateGetValueBody(SimpleNode.java:170)
	at org.apache.ibatis.ognl.SimpleNode.getValue(SimpleNode.java:210)
	at org.apache.ibatis.ognl.ASTNotEq.getValueBody(ASTNotEq.java:49)
	at org.apache.ibatis.ognl.SimpleNode.evaluateGetValueBody(SimpleNode.java:170)
	at org.apache.ibatis.ognl.SimpleNode.getValue(SimpleNode.java:210)
	at org.apache.ibatis.ognl.ASTAnd.getValueBody(ASTAnd.java:56)
	at org.apache.ibatis.ognl.SimpleNode.evaluateGetValueBody(SimpleNode.java:170)
	at org.apache.ibatis.ognl.SimpleNode.getValue(SimpleNode.java:210)
	at org.apache.ibatis.ognl.Ognl.getValue(Ognl.java:333)
	at org.apache.ibatis.ognl.Ognl.getValue(Ognl.java:413)
	at org.apache.ibatis.ognl.Ognl.getValue(Ognl.java:395)
	at org.apache.ibatis.scripting.xmltags.OgnlCache.getValue(OgnlCache.java:45)
	at org.apache.ibatis.scripting.xmltags.ExpressionEvaluator.evaluateBoolean(ExpressionEvaluator.java:29)
	at org.apache.ibatis.scripting.xmltags.IfSqlNode.apply(IfSqlNode.java:30)
	at org.apache.ibatis.scripting.xmltags.MixedSqlNode.apply(MixedSqlNode.java:29)
	at org.apache.ibatis.scripting.xmltags.DynamicSqlSource.getBoundSql(DynamicSqlSource.java:37)
	at org.apache.ibatis.mapping.MappedStatement.getBoundSql(MappedStatement.java:265)
	at org.apache.ibatis.executor.CachingExecutor.query(CachingExecutor.java:79)
	at org.apache.ibatis.session.defaults.DefaultSqlSession.selectList(DefaultSqlSession.java:104)
	... 49 common frames omitted

```

## 网上类似的问题，其实就是mybatis的bug（项目中使用mybatis:3.2.1，需要升级到3.3.0）
- https://blog.csdn.net/qq_41810184/article/details/132543038
- https://github.com/mybatis/mybatis-3/issues/199
- https://github.com/mybatis/mybatis-3/issues/224

