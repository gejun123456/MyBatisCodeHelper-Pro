# MyBatisCodeHelper-Pro

MyBatisCodeHelper-Pro
=================

![Jetbrains Plugins](https://img.shields.io/badge/plugin-9445-orange.svg)
![Version](http://phpstorm.espend.de/badge/9445/version)
![Downloads](http://phpstorm.espend.de/badge/9445/downloads)
![Downloads last month](http://phpstorm.espend.de/badge/9445/last-month)

Intellij下代码自动生成插件 支持生成mybatis的dao接口,mapper xml,和建表sql, 支持直接从接口方法名直接生成sql.
-----------------------------------------------------------------------

付款29元使用Pro版本一年

<img src="http://ogyxv3y5w.bkt.clouddn.com/1499648049347.jpg" width="300">

<img src="http://ogyxv3y5w.bkt.clouddn.com/mm_facetoface_collect_qrcode_1499647909690.png" width="300">

Pro版本与免费版本的区别

- 支持生成多字段索引和多字段唯一
- 支持生成方法 max,min,sum等方法
- 支持生成 findOne,Before,After等语法
- 当查找多个字段时支持生成DTO
- 支持生成接口和接口实现
- 生成的dao不再使用pojo作为param
- 修复byte类型的生成

之后会加入更多功能


 根据接口的方法名直接生成对应的sql
![generateMultiple](http://ogyxv3y5w.bkt.clouddn.com/generate_multiple_method.gif)

 根据数据库对象一键生成 Dao接口，Service，Xml，数据库建表Sql文件  提供dao与xml的跳转
![generateFile](http://ogyxv3y5w.bkt.clouddn.com/generate_multiple_method.gif)


 根据dao中的方法名生成对应的mapper sql并进行方法补全  
![find](http://ogyxv3y5w.bkt.clouddn.com/find.gif)
![update](http://ogyxv3y5w.bkt.clouddn.com/update.gif)
![delete](http://ogyxv3y5w.bkt.clouddn.com/delete.gif)
![count](http://ogyxv3y5w.bkt.clouddn.com/count.gif)
![all_1](http://ogyxv3y5w.bkt.clouddn.com/all_1.gif)

 mybatis接口方法名重构支持
![refacterMethodName](http://ogyxv3y5w.bkt.clouddn.com/refactor_method_name.gif)

#### mybatis xml的自动补全

![autocomplete](http://ogyxv3y5w.bkt.clouddn.com/autoComplete.gif)

#### resultMap refid 跳转到定义和重构

![resultMap](http://ogyxv3y5w.bkt.clouddn.com/resultMapJump.gif)

#### property refid resultMap等的自动补全

![property complete](http://ogyxv3y5w.bkt.clouddn.com/propertyComplete.gif)

安装
----

支持下面产品编译号为141以上的产品。

- Android Studio
- IntelliJ IDEA
- IntelliJ IDEA Community Edition


**使用 IDE 内置插件系统:**
- <kbd>Preferences(Settings)</kbd> > <kbd>Plugins</kbd> > <kbd>Browse repositories...</kbd> > <kbd>搜索并找到"MybatisCodeHelper"</kbd> > <kbd>Install Plugin</kbd>


重启**IDE**.

使用方法
--------------------------------------------------------------------------
- 在数据库对象上使用alt+insert （generate mybatis files）生成对应的dao xml文件等 （mac上使用 ctrl+N 即getter setter对应的快捷键)
- 当数据库对象添加字段后也可使用alt+insert （generate mybatis files）来生成更新后的xml。（只会更新默认的insert,insertList,update方法 其他自定义的方法不会变）
- 在mybatis的接口文件上的方法名上使用alt+enter generatedaoxml 生成对应的mybatis sql及方法的补全


需要注意的点
-----------------------------------------------------------------------------

- 使用方法名生成sql 需要在接口中提供一个insert或save或add方法并以数据库对象为第一参数 (可以通过数据库对象自动生成)
- 使用方法名生成的sql的字段会从数据库对象对应的resultMap中的数据库字段来设置。

现在支持的数据库对象字段类型

| 字段类型            |  开始支持的版本        |
|----------------------|-------------------  |
| java.lang.Integer    |   v1.2              |
| java.lang.Long       |   v1.2              |
| java.lang.FLoat      |   v1.2              |
| java.lang.Double     |   v1.2              |
| java.lang.Boolean    |   v1.2              |
| java.util.Date       |   v1.2              |
| java.lang.String     |   v1.2              |
| java.lang.Byte       |   v1.2              |
| java.math.BigDecimal |   v1.2              |
| java.lang.Short      |   v1.2              |




方法名生成sql
-----------------------------------------------------------------------------------------
数据库对象User

字段名  | 类型
-----   | ------
id      | Integer
userName | String
password | String

表名为user

xml中对应的resultMap为

	<resultMap id="AllCoumnMap" type="com.codehelper.domain.User">
	    <result column="id" property="id"/>
	    <result column="user_name" property="userName"/>
	    <result column="password" property="password"/>
	</resultMap>


以下是方法名与sql的对应关系(方法名的大小写无所谓)


可以跟在字段后面的比较符有

比较符  | 生成sql
------- | --------
between |  prop > {} and prop <{}
betweenOrEqualto | prop >={} and prop <={} v1.3
lessThan  | prop < {}
lessThanOrEqualto | prop <={}  v1.3
greaterThan | prop > {}
greaterThanOrEqualto | prop >={}  v1.3
isnull | prop is null
notnull | prop is not null
like   | prop like {}
in     | prop in {}
notin  | prop not in {}
not    | prop != {}
notlike | prop not like {}

- find方法

支持获取多字段，by后面可以设置多个字段的条件 一个字段后面只能跟一个比较符
支持orderBy,distinct, findFirst

方法名       |  sql
-----------  |  --------------
find         | select * from user
findUserName | select user_name from user
findById	| select * from user where id = {}
findByIdGreaterThanAndUserName | select * from user where id > {} and user_name = {}
findByIdGreaterThanOrIdLessThan | select * from user where id > {} or id < {}
findByIdLessThanAndUserNameIn  | select * from user where id < {} and user_name in {}
findByUserNameAndPassword      | select * from user where user_name = {} and password = {}
findUserNameOrderByIdDesc   | select user_name from user order by id desc
findDistinctUserNameByIdBetween | select distinct(user_name) from user where id >= {} and id <={}
findFirstByIdGreaterThan | select * from user where id > {} limit 1
findFirst20ByIdLessThan  | select * from user where id < {} limit 20
findFirst10ByIdGreaterThanOrderByUserName  | select * from user where id > {} order by user_name limit 10

- update方法 by后面设置的条件同上

方法名     | sql
---------- |  -------
updateUserNameById | update user set user_name = {} where id = {}
updateUserNameAndPasswordByIdIn  | update user set user_name = {} and password = {} where id in {}

- delete方法
by后面设置的条件同上

方法名  |  sql
------- | ---------
deleteById | delete from user where id = {}
deleteByUserNameIsNull  | delete from user where user_name is null

- count方法
by后面设置的条件同上 支持distinct

方法名  | sql
------- | ----------
count   | select count(1) from user
countDistinctUserNameByIdGreaterThan | select count(distinct(user_name)) from user where id > {}



CHANGELOG
------------------------------------------------

1.6.0
- 支持生成多字段索引和多字段唯一
- 支持生成方法 max,min,sum等方法
- 支持生成 findOne,Before,After等语法
- 当查找多个字段时支持生成DTO
- 支持生成接口和接口实现
- 生成的dao不再使用pojo作为param
- 修复byte类型的生成

1.4.2
- 支持oracle
- 配置使用useGenerateKey
- resultMap refid keyProperty if test的自动补全
- 支持java8 time里的类型
- 添加新图标
- 在通过方法名生成sql如果接口引入其他类型比如（java.util.Date)自动import到接口中
- bugfix 修复生成文件为null和initialize class com.ccnode.codegenerator.freemarker.TemplateUtil exception(大部分mac会出现的问题)

1.3
- 生成mybatis文件时可生成索引及选择是否需要默认值
- 生成mybatis文件加入insertSelective
- 在配置中可选择mybatis接口是否加上@Mapper注解
- 方法名生成sql 支持greaterThanOrEqualTo lessThanOrEqualTo betweenOrEqualto
- 支持resultMap refid跳转至定义及重构
- 支持xml中的方法名重构
- 修复module为空的警告


1.2
- 添加mapper与dao的相互跳转
- 使用alt+insert生成xml
- 添加方法名生成sql
- 添加方法名自动提示
----------------------------------
- 加入qq群
![qqGroup](http://ogyxv3y5w.bkt.clouddn.com/qqgroup.png)


截图中的项目来自[https://github.com/gejun123456/codehelperPluginDemo](https://github.com/gejun123456/codehelperPluginDemo)



