## mybatis console log to sql

### idea console need to print mybatis log
- make sure console print mybatis log

![mybatislogsupport](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/mybatisLogSupportNew2.gif)

make sure console log contains prepare and parameter

if not, you need to config log 

log4j2 configuration:

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
Or
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







