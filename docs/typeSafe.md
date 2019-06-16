#  构建安全的mybatis sql

## IDEA高级版提供了sql自动补全 sql语法检测， IDEA高级版可以写出安全的sql 如下图
![idea自带的database自动补全和检测和运行sql](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/idea自带的database自动补全和检测和运行sql.gif)

对于使用mybatis 会导致sql错误 可能以下几种原因
1. sql中使用了mybatis的动态标签 include trim set where foreach
2. 使用了if test choose when条件判断
3. if test when bind中的判断语句错误
4. #{} foreach collection中的语句错误

## 2.0.1版本后的插件便可以识别include trim set where foreach标签，使用了标签的sql可以进行检测和自动补全
比如对于trim标签



