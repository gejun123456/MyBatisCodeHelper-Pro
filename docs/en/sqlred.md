## How to handle with sql error problem.

Set up database and sql dialect in https://gejun123456.github.io/MyBatisCodeHelper-Pro/#/configure


### sql tag error, sql in mybatis sql is not complete, inspection and completion cant work，Plugin introduced @sql comment，set up sql prefix and suffix in the comment, so the sql is complete, inspection and completion will work fine.

![sqlTagNoError](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/sqlTagNoError.gif)

If there is referenced select statement for sql tag, you can just alt enter the generate the @sql comment.
![addSqlComment](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/addSqlComment.gif)

### when using if test, choose when May some of the condition is passed. only one pass in choose when. The plugin introduced @ignoreSql comment，if you need if test or choose when statment not pass, you can use it, so the sql will be correct.

Add ignore comment
![chooseWhenAutoComplete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/chooseWhenAutoComplete.gif)

### for ${} statement, the part can be any string, the sql can't be recognized. The plugin introduced $sql commment, you can add your real sql into the $sql comment to make sql correct. Sql statement after ${} can be recognized.

add real sql for ${} expression
![parse$byXmlTagComment](https://images.brucege.com/parse$byXmlTagComment.gif)

(Add sql representation for $ statement))
![AddSqlAfter$](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/AddSqlAfter$.gif)
