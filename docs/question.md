## 如何生成的时候返回主键id？

首先要确保主键是自动生成的，比如 mysql主键 设置为 autoIncrement
然后 数据库在生成的时候 填写了 useGeneratedKey为你的主键字段名
之后在生成的接口会有一个insert方法 比如  insert(User user)  生成的xml中的insert 语句 会有
useGeneratedKey = true
在执行完插入语句后 可以使用 user.getId() 来获取生成的id

## 我不想要xml的注释怎么处理

通过数据库生成时，xml里面会有一系列 @Mbg generated的这种注释，这个注释的目的是让人知道这个是自动生成的，并且可以在数据库添加了字段重新生成的时候 只会更新 xml中标记了这些注释的语句，所以建议还是生成注释比较好

如果还是不想要注释 可以在数据库生成的时候 有一个 genComment选项 把它关闭就不会生成了

## 如何进行逻辑删除

目前在生成代码的时候还没有提供默认生成逻辑删除的语句 
可以先通过方法名来进行生成
可以写 updateIsDeleteById 来生成 通过主键逻辑删除

## xml param 中的 jdbcType 有啥用

https://stackoverflow.com/questions/18645820/is-jdbctype-necessary-in-a-mybatis-mapper

部分数据库在插入 删除 更新的时候 如果传的是null值 需要添加jdbcType  加上jdbcType是更安全的做法

经测试 mysql不需要 oracle需要 

## 怎么生成 if test 怎么换图标 方法名生成的代码怎么弄到service中

设置里面可以配置 

![setting](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/settings.png ':size=100%')

