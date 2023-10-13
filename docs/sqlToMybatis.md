## 从sql生成好mybatis的xml和java接口方法（3.2.5)

### 从IDEA的console sql上面右键 使用
![convertSqlToMybatis](https://images.brucege.com/convertSqlToMybatisStatement.png)

在配置的界面，可以选择需要改成的参数:
![convertsqlToMybatisSetting](https://images.brucege.com/convertSqlToMybatisConfigPage.png)

### 最后的结果
![sqlToMybatis](https://images.brucege.com/sql%E5%BF%AB%E9%80%9F%E8%BD%ACxml%E5%92%8C%E6%8E%A5%E5%8F%A3%E6%96%B9%E6%B3%95.gif)

### 目前还没有直接生成resultmap,生成好了后,可以使用 xml生成java类和resultmap功能来生成对应的结果映射

## 3.2.6优化了接口参数类型,会根据字段类型来进行判断，可以在群文件中下载到
