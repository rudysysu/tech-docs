## 代码报错
java.sql.SQLException: Unknown connection id:73316544 used:5737

## 问题分析

### 错误日志
```
java.sql.SQLException: Unknown connection id:73316544 used:5737
...
Caused by: java.sql.SQLException: Unknown connection id:73316544
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:996)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3887)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3823)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2435)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2582)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2526)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2484)
	at com.mysql.jdbc.StatementImpl.execute_aroundBody2(StatementImpl.java:848)
	at com.mysql.jdbc.StatementImpl$AjcClosure3.run(StatementImpl.java:1)
	at org.aspectj.runtime.reflect.JoinPointImpl.proceed(JoinPointImpl.java:149)
	at com.mysql.jdbc.StatementImpl.execute(StatementImpl.java:746)
	at com.mysql.jdbc.StatementImpl.execute_aroundBody0(StatementImpl.java:742)
	at com.mysql.jdbc.StatementImpl$AjcClosure1.run(StatementImpl.java:1)
	at org.aspectj.runtime.reflect.JoinPointImpl.proceed(JoinPointImpl.java:149)
	at com.mysql.jdbc.StatementImpl.execute(StatementImpl.java:742)
	at com.mysql.jdbc.StatementImpl$CancelTask$1.run(StatementImpl.java:119)
```

### MyBastis超时配置
```
<select id="getPropsRecvHistory" resultMap="BaseResultMap" timeout="5">
```

### 类似问题
https://juejin.cn/post/7018084382745296927

### 问题结论
- StatementImpl对于超时的SQL，会启动CancelTask任务，调用MySQL服务，KILL掉对应的线程。
- 但是数据库代理存在BUG，不支持KILL超时线程，具体原因是：
  - 代理返回给业务代码是替换后的线程ID，不是真正的数据库线程ID
  - KILL 线程ID的时候，数据库代理没有做对应的替换，所以数据库不认识这个ID。
