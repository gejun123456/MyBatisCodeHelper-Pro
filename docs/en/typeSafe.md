#  Type Safe sql support

## IDEA ultimate version provide safe sql support

![idea自带的database自动补全和检测和运行sql](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/idea自带的database自动补全和检测和运行sql.gif)

## With Mybatis, There are some case that sql is not safe.
- use mybatis dynamic tag. include trim set where foreach bind.
- use if test choose when for condition
- ognl statement error. if test when bind ${} foreach collection
- error in #{}
- sql in ```<sql></sql>```

## plugin can recognize include trim set where foreach tag, you can gain auto complete and inspection when using those.
like trim tag
![trim标签正确性检测](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/trim标签正确性检测.gif)

set tag.
![set标签正确性](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/set标签正确性.gif)

## when using if test, May some of the condition is passed. only one pass in choose when. The plugin introduced @ignoreSql comment，if you need if test or choose when statment not pass, you can use it, so the sql will be correct.

![chooseWhenAutoComplete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/chooseWhenAutoComplete.gif)

## when write if test when bind ${} foreach collection, the plugin has full support for ognl statment.

if test when test

![ifWhenTest中ognl支持](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/ifWhenTest中ognl支持.gif)

bind and ${

![bind和${的ognl支持](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/bind和${的ognl支持.gif)

for ${} statement, the part can be any string, the sql can't be recognized. The plugin introduced $sql commment, you can add your real sql into the $sql comment to make sql correct. Sql statement after ${} can be recognized.

![AddSqlAfter$](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/add$sql.gif)

or add real sql for ${} expression
![parse$byXmlTagComment](https://images.brucege.com/parse$byXmlTagComment.gif)

foreach collection

![collection标签跳转检测正确](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/collection标签跳转检测正确.gif)

## Plugin support for param statement.

![检测param是否正确](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/检测param是否正确.gif)

## sql tag error, for sql tag, the sql is complete, The plugin introduce @sql comment, you can add them to sql prefix and sql suffix, to make sql tag a correct sql. 
![sqlTagNoError](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/sqlTagNoError.gif)

The difference between @sql and $sql is if @sql comment is from include refid wont be parsed. If one select statement include one sql, your @sql comment in the include sql won't be parsed, but $sql will be parsed. 

## There are other inspection and completion like resultMap column and property. 

## The plugin will continue to make mybatis development fast and enjoyable.
