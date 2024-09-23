## sql标红如何处理

首先确保配置好数据库和dialect 参照文档 https://gejun123456.github.io/MyBatisCodeHelper-Pro/#/configure


### sql标签中的字段标红 sql标签中的sql 由于不是完整的sql，无法进行检测和代码补全，插件引入了 @sql 注释，在注释中把sql的前缀和后缀填写进去，可保证sql标签中的sql无误  

![sqlTagNoError](https://images.brucege.com/sqlTagNoError.gif)

### 如果sql标签有引用的select语句 可以直接alt enter来生成注释  

![addSqlComment](https://images.brucege.com/addSqlComment.gif)

### choose when语句没有自动提示，标红。由于choose when只有一个生效，使用ignore注释将其他的when语句给忽略掉，用于自动补全和提示  

请添加ignore注释 参考
![chooseWhenAutoComplete](https://images.brucege.com/chooseWhenAutoComplete.gif)

### 在编辑choose when时，可以把其他when语句设置为ignore，这样写when语句会有代码提示和检测，效率高一些


### 使用${}的sql会标红

由于$中可以使用任意的字符串，无法解析具体的sql是啥，插件没有将${}加入sql解析，可以在${}的后面添加一个注释代表真正可能的sql，比如引用常量的时候，需要把常量的值放到注释中
，这样$不会标红并且后面的sql也能正确识别

或者在xml的标签上加一个$注释 这种可以解析多个${}
![parse$byXmlTagComment](https://images.brucege.com/parse$byXmlTagComment.gif)

(2.7.6支持一键生成对应的sql)
![AddSqlAfter$](https://images.brucege.com/AddSqlAfter$.gif)
