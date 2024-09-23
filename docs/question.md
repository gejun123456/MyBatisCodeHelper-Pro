## 如何生成的时候返回主键id？

首先要确保主键是自动生成的，比如 mysql主键 设置为 autoIncrement
oracle 主键添加序列和触发器 (用java类生成建表语句可以自动生成好)
(2.7.6支持配置oracle序列)
然后 数据库在生成的时候 填写了 useGeneratedKey为你的主键字段名
之后在生成的接口会有一个insert方法 比如  insert(User user)  生成的xml中的insert 语句 会有
useGeneratedKey = true
在执行完插入语句后 可以使用 user.getId() 来获取生成的id

## 生成代码出现 can't find xml file for namespace xxxx
先查看xml中的namespace是否与接口一致，如果一致， 查看是否安装了其他冲突插件如FreeMybatisPlugin,MybatisX,MybatisPlugin(mybatisLogPlugin不冲突),如果有请卸卸掉 然后使用 invalidate Cache and restart. https://images.brucege.com/invalidateCacheAndRestart.png
如果还没有发现问题，请查看下 接口和xml 是否在同一个module，module是否有依赖关系，如果在同一个module还有问题，请联系我


## mybatis generator没有生成service接口 (2.6版本可以生成)

一般spring项目中service接口没啥用 参考 https://www.zhihu.com/question/296829023/answer/521249348

如果实在要接口 可以使用Intellij自带的一键导出接口 https://images.brucege.com/extractInterface.png

## 我不想要xml的注释怎么处理

通过数据库生成时，xml里面会有一系列 @Mbg generated的这种注释，这个注释的目的是让人知道这个是自动生成的，并且可以在数据库添加了字段重新生成的时候 只会更新 xml中标记了这些注释的语句，所以建议还是生成注释比较好

如果还是不想要注释 可以在数据库生成的时候 有一个 genComment选项 把它关闭就不会生成了

## 数据库加减字段后如何重新生成
1.首先通过数据库生成的时候选中 genComment(默认选中) 会生成一些自带方法，请不要修改这些自动生成的方法 这些方法会在第二次生成的时候给新方法覆盖掉
2.数据库加减或修改字段重新从数据库生成下即可，不会覆盖掉你自己加的自定义方法这些 xml mapper接口 service 都会自动合并好

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

![setting](https://images.brucege.com/settings.png)


## 方法名生成sql时 出现 please check with your xml resultMap id:  dose it contain all the property of resultMap 怎么处理

出现该异常的原因是 xml中的resultMap 和 resultMap type中 对应的实体的属性不一致  xml的resultMap中缺少了一些字段

由于方法名生成sql 需要知道实体里面 每个属性 对应的数据库字段名

要么在 resultMap中添加缺少的属性  或者 在java实体中 将这个属性 设置为 transient

有一些java实体中 会有一些属性是从其他表查出来的  比如 Blog类 里面有一个 List<Commnet>

这种情况 用 transient 也不合适， 建议更改继承关系 不要把List<Comment>放到 Blog中  而是加一个 BlogWithComment的类 继承 Blog类。

请不要更改自动生成的BaseResultMap.

## 数据库 添加字段后 如何生成

直接使用 mybatis generator 重新生成即可 会保留接口和xml中不是自动生成的方法


## 我的model类中添加了其他字段，重新生成的时候被覆盖了

可以将自己添加的字段设置为transient类型，就不会覆盖了
即private transient String moreField 或者添加@javax.persistence.Transient注解
如果找不到该注解 请添加maven依赖

```
<dependency>
    <groupId>javax.persistence</groupId>
    <artifactId>javax.persistence-api</artifactId>
    <version>2.2</version>
</dependency>
```


## mybatis在写sql时数据库字段没有自动提示
使用Intellij高级版 需要配置idea自带的database 在配置的时候记得填上数据库名

## 使用模版如cd co ${ ignore sql报错Range Marker Error
出现提示后请用tab键 而不是enter键来进行补全，这个是IDEA的一个bug 以后看看

## 从表生成代码只有两个insert方法
请检查表中是否有主键，如果有主键请刷新IDEA的数据库 直到下图这种
![tableNoPrimaryKey](https://images.brucege.com/tableNoPrimaryKey.png)


## 如何配置java文件的header注释 
![header](https://images.brucege.com/header.png)


![tableNoPrimaryKey](https://images.brucege.com/tableNoPrimaryKey.png)

## sql标签中的字段标红 sql标签中的sql 由于不是完整的sql，无法进行检测和代码补全，插件引入了 @sql 注释，在注释中把sql的前缀和后缀填写进去，可保证sql标签中的sql无误

![sqlTagNoError](https://images.brucege.com/sqlTagNoError.gif)

## choose when语句 没有自动提示，标红

请添加ignore注释 参考
![chooseWhenAutoComplete](https://images.brucege.com/chooseWhenAutoComplete.gif)

## 使用${}的sql会标红

由于$中可以使用任意的字符串，无法解析具体的sql是啥，插件没有将${}加入sql解析，可以在${}的后面添加一个注释代表真正可能的sql，比如引用常量的时候，需要把常量的值放到注释中
，这样$不会标红并且后面的sql也能正确识别

(2.7.6支持一键生成对应的sql)
![AddSqlAfter$](https://images.brucege.com/AddSqlAfter$.gif)

## 数据库表是tinyint(1)生成了boolean类型

mysql tinyint(1)与boolean是一个含义，不想生成boolean请使用tinyint(4)


## 怎么去掉sql显示中的黄色背景


![yellowBackGround](https://images.brucege.com/yellowBackGround.png)

## 生成的xml中的@Table有什么用

table注释用于 当 xml中没有insert方法时 指定了xml对应的表名，插件便可以解析BaseColumnList为表中的字段，另外在方法名生成sql的时候不再需要依赖一个insert方法了.


## 2019.3及以上版本，写sql表和列名没有自动提示

看文档配置数据那节，记得设置里面配置好dialect

## 想用模版来生成
可以使用 https://github.com/gejun123456/easyCode-MybatisCodeHelper。

## 插件生成testcase 配置文件只会加载当前的接口对应的xml，如果引用了其他xml需要自己添加一下
在生成testcase的setUp方法会引用一个xml文件，在xml文件中添加引用的xml位置
![testcaseAddMapperResource](https://images.brucege.com/testcaseAddMapperResource.png)


## 2.8.2后代码格式化未生效 多出空行
请参考文档配置数据库那节，照着配置下，确保sql dialect配置好 https://gejun123456.github.io/MyBatisCodeHelper-Pro/#/configure

## 2.8.2 BaseResultMap中的column标红了
原因了引用的resultmap的select语句没有查对应的column，比如BaseResultMap有5个字段，但是select只查了4个字段这种。
可以随便弄个方法名比如findById查所有字段那种就可以解决或者单独抽一个ResultMap出来。
下个版本做个兼容。

## mybatis注解有支持吗？
由于mybatis注解功能较弱，不支持resultMap的复用，并且复杂sql多的时候难以维护。    
插件对简单的注解sql有代码提示,script标签中的注解sql也有代码提示，if test代码提示，  
但是还不支持script标签使用collection等内部的提示，建议太长的注解使用xml来写

## 使用cdata导致后面的代码没有自动提示
可以把cdata中的小于号大于号给替换为&lt;和&gt;即可,插件也提供了一个alt enter 可以一键替换cdata中的小于号大于号特殊字符


## idea社区版部分数据库无法连接 无法生成代码
请加入qq群516959916 里面有专门支持社区版的插件，支持各种数据


## 如何设置插件为中文
可以尝试以下途径
1. 在idea中安装中文支持插件
2. 把操作系统的语言设置为中文
3. 设置vmOption添加 -Duser.language=zh -Duser.region=CN
一般会变成中文，有问题请再联系我

## 从其他Mybatis插件迁移到该插件 
1. 之前公司使用的MybatisX的代码生成器，配置好了模板等，但是插件不兼容导致不能使用之前的代码生成
可以使用：https://github.com/gejun123456/mybatisX-CodeGeneratorOnly




## 和其他插件对比
插件拥有最好的mybatis sql代码提示，代码检测，重构，泛型支持，typeAlias支持，快速测试sql，方法名生成sql等。
可以参考
https://brucege.com/doc/#/typeSafe
