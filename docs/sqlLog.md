## mybatis日志转sql功能

### idea控制台需要打印mybatis的日志 
- 先检查控制台是否打印了mybatis的日志 如下图

![mybatislogsupport](https://images.brucege.com/mybatisLogSupportNew2.gif)

请确保idea控制台中包含 prepare 和 parameter 如上图

如果没有，可以配置一下项目使用的日志框架，可以把 logLevel配置为debug

log4j2配置如下，Root Level为debug或者单独配置mybatis接口的包名，其他日志框架也类似：

com.mapper 为mybatis接口的包名
```
<?xml version="1.0" encoding="UTF-8"?>
<Configuration xmlns="http://logging.apache.org/log4j/2.0/config">
    <Appenders>
        <Console name="stdout" target="SYSTEM_OUT">
            <PatternLayout pattern="%c %5level [%t] - %msg%n"/>
        </Console>
    </Appenders>

    <Loggers>
        <Logger name="com.mapper" level="DEBUG"/>
        <Root level="INFO">
            <AppenderRef ref="stdout"/>
        </Root>
    </Loggers>
</Configuration>
```
或者直接配置为debug 日志量会变多
```
<?xml version="1.0" encoding="UTF-8"?>
<Configuration xmlns="http://logging.apache.org/log4j/2.0/config">
    <Appenders>
        <Console name="stdout" target="SYSTEM_OUT">
            <PatternLayout pattern="%c %5level [%t] - %msg%n"/>
        </Console>
    </Appenders>

    <Loggers>
        <Root level="DEBUG">
            <AppenderRef ref="stdout"/>
        </Root>
    </Loggers>
</Configuration>
```

### 在idea的日志中，点击parameter就可以跳转到最终的sql

### 如果sql太长比如一条sql超过20000字符，插件为了避免性能影响这个时候不能点击parameter跳转，可以把sql拷到TextToConvert框那里进行识别

![sql太长](https://images.brucege.com/MybatisLogTextToConvert.png)

### 如果你的参数包含换行符，可以用sql and parameter 那里，把sql和参数拷到那里进行识别


### 从日志跳转到xml (3.1.3版本)

确保log配置打印了class信息

log4j2配置如下
```xml
<?xml version="1.0" encoding="UTF-8"?>
<Configuration xmlns="http://logging.apache.org/log4j/2.0/config">
    <Appenders>
        <Console name="stdout" target="SYSTEM_OUT">
            <PatternLayout pattern="%c %5level [%t] - %msg %n  "/>
        </Console>
    </Appenders>

    <Loggers>
        <Root level="DEBUG">
            <AppenderRef ref="stdout"/>
        </Root>
    </Loggers>
</Configuration>
```

将类名.方法名 打印在最前面才可以识别
log4j2 PatternLayOut 开始有一个%c 打印当前类的信息，打印的日志如下

logback 用%logger 或者%c 打印当前类的信息


```text
org.apache.ibatis.logging.LogFactory DEBUG [main] - Logging initialized using 'class org.apache.ibatis.logging.log4j2.Log4j2Impl' adapter. 
  org.apache.ibatis.transaction.jdbc.JdbcTransaction DEBUG [main] - Opening JDBC Connection 
Mon Nov 14 11:25:27 CST 2022 WARN: Establishing SSL connection without server's identity verification is not recommended. According to MySQL 5.5.45+, 5.6.26+ and 5.7.6+ requirements SSL connection must be established by default if explicit option isn't set. For compliance with existing applications not using SSL the verifyServerCertificate property is set to 'false'. You need either to explicitly disable SSL by setting useSSL=false, or set useSSL=true and provide truststore for server certificate verification.
  com.bruce.ggg.AdminMapper.findByAdminNameAndAdminPwd DEBUG [main] - ==>  Preparing: SELECT admin_id, admin_name, admin_pwd, `status`, real_name, telephone, create_time, update_time, center_id, admin_type, myDate FROM `admin` where admin_name LIKE ? ORDER BY admin_id DESC  
  com.bruce.ggg.AdminMapper.findByAdminNameAndAdminPwd DEBUG [main] - ==> Parameters: 74(Integer) 
  com.bruce.ggg.AdminMapper.findByAdminNameAndAdminPwd DEBUG [main] - <==      Total: 0 
```

确保以类名为开头的日志，如上图，可以看到com.bruce.ggg.AdminMapper.findByAdminNameAndAdminPwd

然后在mybatis sql控制台中，看看日志的注释中是否有类名信息，选中日志，按右键jumpToXml，即可跳转到xml

![jumpToXml](https://images.brucege.com/jumpToXml.png)







