## 根据mybatis接口中的方法名生成对应的mapper sql并进行方法补全  支持通用mapper mybatisplus

只需要一个方法名 即可 不需要方法和参数 和返回值 输入方法名后 alt+enter 就可以生成了

![generateMultiple](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/fromMethodName.gif)

![find](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/2017_08_06_find_example_2.gif)

![update](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/update.gif)


![delete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/delete.gif)


![count](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/count.gif)

![all_1](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/all_1.gif)


## 方法名生成sql时支持if test ( 新版本无需配置 直接alt+enter generate method to sql with if test即可)

![if-test](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/mybatis_generate_if_test.gif)


## 一键生成findByAll

![findByAll]](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/support_find_by_all.gif)


## 一键生成insertList
![insertList]](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/methodNameCouldGenerateInsertList.gif)

## 使用方法  
- 在mybatis的接口文件上的方法名(只需要一个名字，不需要返回值和参数 会自动推导出来)上使用alt+enter gendaoxml 或者选中方法名右键来生成


## 方法名的规则


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

比较符  | 生成sql | 开始支持的版本号
------- | -------- |---------
between |  prop > {} and prop <{}  |v1.3
betweenOrEqualto | prop >={} and prop <={} | v1.3
lessThan  | prop < {} | v1.3
lessThanOrEqualto | prop <={}  |v1.3
greaterThan | prop > {} |v1.3
greaterThanOrEqualto | prop >={} | v1.3
isnull | prop is null |v1.3
notnull | prop is not null |v1.3
like   | prop like {} |v1.3
in     | prop in {} |v1.3
notin  | prop not in {} |v1.3
not    | prop != {} |v1.3
notlike | prop not like {} |v1.3
startingWith | prop like {}% |v1.6.0
endingWith | prop like %{} |v1.6.0
containing | prop like %{}% |v1.6.0
true       | prop = true | 2.0
false      | prop = false |2.0
lessThanEqual| prop <= {} | 2.0
greaterThanEqual | prop >={}|2.0



- find方法  可以使用 select query get 替代find开头

支持获取多字段，by后面可以设置多个字段的条件 一个字段后面只能跟一个比较符 
支持orderBy,distinct, findFirst

方法名       |  sql
-----------  |  --------------
find         | select * from user
findUserName | select user_name from user
findById	| select * from user where id = {}
findUserNameById | select user_name from user where id = {}
findByIdGreaterThanAndUserName | select * from user where id > {} and user_name = {}
findByIdGreaterThanOrIdLessThan | select * from user where id > {} or id < {}
findByIdLessThanAndUserNameIn  | select * from user where id < {} and user_name in {}
findByUserNameAndPassword      | select * from user where user_name = {} and password = {}
findUserNameOrderByIdDesc   | select user_name from user order by id desc
findDistinctUserNameByIdBetween | select distinct(user_name) from user where id >= {} and id <={}
findOneById	| select * from user where id = {}
findFirstByIdGreaterThan | select * from user where id > {} limit 1
findFirst20ByIdLessThan  | select * from user where id < {} limit 20
findFirst10ByIdGreaterThanOrderByUserName  | select * from user where id > {} order by user_name limit 10
findMaxIdByUserNameGreaterThan | select max(id) from user where user_name > {}
findMaxIdAndMinId   | select max(id) as maxId, min(id) as minId from user


- update方法 by后面设置的条件同上 可以使用modify替代update开头

方法名     | sql
---------- |  -------
updateUserNameById | update user set user_name = {} where id = {}
updateUserNameAndPasswordByIdIn  | update user set user_name = {} and password = {} where id in {}
updateIncVersionByIdAndVersion | update user set version = version+1 where id = {} and version = {}

- delete方法  可以使用remove替代delete开头
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


## 注意的点  

- 使用方法名生成sql 需要在接口中提供一个insert或save或add方法并以表对应的java对象为第一参数 (类似于 insert(User user) 需要通过User来进行方法名的推断) 使用了通用mapper或者mybatisplus的话 不需要insert方法
- 使用方法名生成的sql的字段会从数据库对象对应的resultMap中的数据库字段来设置。

- "please check with your resultMap dose it contain all the property of 
此时可以检查这个接口对应的对象 比如 这个接口有个 insert(User user) 即 User对象
是否有一个对应的完整的resultMap在xml中，resultMap中少了属性的话 无法生成 可以将属性设置为transient类型

- 当生成sql时 如果比如UserMapper对应的User对象中含有List或Set类型的属性时，sql会无法生成
请将这些属性设置为transient类型  比如 private transient List<Comment>

- 我写了find后方法名没有自动提示如何处理?

查看IDEA设置里的completion 是否设置为 firstLetter
![compele](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/completeSetting.png)
