## Using Mapper method name to generate sql. Only need a method name, no need for method parameters and return type.

![findMethodNameToSql](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/findMethodNameToSql.gif)

![updateMethodNameToSql](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/updateMethodNameToSql.gif)

![deleteMethodNameToSql](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/deleteMethodNameToSql.gif)

![countMethodNameToSql](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/countMethodNameToSql.gif)


## Method generate sql support generate if test.

![findWithIfTest](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/findWithIfTest.gif)


## Generate findByAll

![findByAllEE](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/findByAllEE.gif)

## Generate insertList
![insertList](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/insertList.gif)

## How use

- select method name and right click on it, select generatedaoxml,  you just need a valid method name, no need to return name and parameters.



## Rule

Java class User

Field  | JavaType
-----   | ------
id      | Integer
userName | String
password | String

tableName is user

the result map in xml is

	<resultMap id="BaseColumnList" type="com.codehelper.domain.User">
	    <result column="id" property="id"/>
	    <result column="user_name" property="userName"/>
	    <result column="password" property="password"/>
	</resultMap>


following is the generated sql by the mapper method name (method name using upper and lower case is the same for generate)


the comparator after fields are following.

Comparator  |Generated sql | Start support version
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




- find   could use select query get to repalce find
support orderBy,distinct, findFirst

methodName       |  sql
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


- update  could use modify to replace update

methodName     | sql
---------- |  -------
updateUserNameById | update user set user_name = {} where id = {}
updateUserNameAndPasswordByIdIn  | update user set user_name = {} and password = {} where id in {}
updateIncVersionByIdAndVersion | update user set version = version+1 where id = {} and version = {}

- delete  could use remove to replace delete.

methodName  |  sql
------- | ---------
deleteById | delete from user where id = {}
deleteByUserNameIsNull  | delete from user where user_name is null

- count

methodName  | sql
------- | ----------
count   | select count(1) from user
countDistinctUserNameByIdGreaterThan | select count(distinct(user_name)) from user where id > {}


## Rules 

- When use method name to generate sql, you need to hava an Insert or add 
like insert(User user) in your mapper method. Cause User is needed to support springdataJpa like language.
- MethodName to sql current only support generate in xml files, you need to set up a xml file first, you can
generate it by alt+enter on mapper interface class name.
- If you have xml and you have insert method but the method name completion not work, please make sure your completion
setting is same to following.

![compele](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/completeSetting.png)

