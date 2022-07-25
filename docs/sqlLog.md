## mybatis日志转sql功能

### idea控制台需要打印mybatis的日志 
- 先检查控制台是否打印了mybatis的日志 如下图

![mybatislogsupport](https://myimages.brucege.com/mybatisLogSupportNew2.gif)

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







