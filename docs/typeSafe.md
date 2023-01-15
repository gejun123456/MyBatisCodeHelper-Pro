#  构建安全的mybatis sql（插件2.8.0版本）(插件原创功能)

## 可以先看视频：https://www.bilibili.com/video/BV1PB4y167N1

## IDEA高级版提供了sql自动补全 sql语法检测， IDEA高级版可以写出安全的sql 如下图
![ideaInnerSupport](https://images.brucege.com/ideaInnerSupport.gif)

## 对于使用mybatis 会导致sql错误 可能以下几种原因
1.  sql中使用了mybatis的动态标签 include trim set where foreach
2.  使用了if test choose when条件判断
3.  if test when bind ${} foreach collection中的判断语句错误
4.  #{} 中的语句错误

### 插件可以识别include trim set where foreach标签，使用了标签的sql可以进行检测和自动补全
比如对于trim标签
![trim标签正确性检测](https://images.brucege.com/trim标签正确性检测.gif)

set标签
![set标签正确性](https://images.brucege.com/set标签正确性.gif)

### 当使用if test时 可能只有部分条件成立 choose when 则只有一个条件成立 插件引入了 @ignoreSql 注释，如果需要if test 或choose when 不成立可以使用该注释，检测sql是否正确和代码提示

![chooseWhenAutoComplete](https://images.brucege.com/chooseWhenAutoComplete.gif)

### 当我们写if test when bind ${} foreach collection中的语句也可能会出错，这块语法是使用的ognl语法，插件对这块进行了支持

if test when test
![ifWhenTest中ognl支持](https://images.brucege.com/ifWhenTest中ognl支持.gif)

bind和 ${
![bind和${的ognl支持](https://images.brucege.com/bind和${的ognl支持.gif)

bind进行绑定变量的类型推断支持

![ognl method call](https://images.brucege.com/collectionCallMethdo.gif)


对于 ${ 由于里面的输入可以是任意字符，sql会无法解析，插件引入了 $sql注释，如下图，真正要被替换的语句写入$sql 注释中$后的sql也可正常代码提示了
![AddSqlAfter$](https://images.brucege.com/add$sql.gif) 

或者在xml的标签上加一个$注释 这种可以解析多个${}
![parse$byXmlTagComment](https://images.brucege.com/parse$byXmlTagComment.gif)

foreach collection
![collection标签跳转检测正确](https://images.brucege.com/collection标签跳转检测正确.gif)

### 在2.5版本后 插件便可以对 #{}中的内容进行检测是否正确
![检测param是否正确](https://images.brucege.com/检测param是否正确.gif)

### 另外在sql标签中的sql 由于不是完整的sql，无法进行检测和代码补全，插件引入了 @sql 注释，在注释中把sql的前缀和后缀填写进去，可保证sql标签中的sql无误
![sqlTagNoError](https://images.brucege.com/sqlTagNoError.gif)

@sql和$sql的唯一区别是 如果@sql如果是通过 include refid引入的时候的不会被解析. 如在一个select引入include时 不会对include中的@sql注释的sql解析，但会对$sql解析

### 插件在2.7版本引入了3个注释 @ignoreSql @sql $sql来保证条件sql的正确性，添加了ognl支持 防止 if test bind ${ foreach collection中的内容出错，基本可以保证sql不再出错了。

### 2.7版可能出现的问题

1. if test等中的ognl表达式只支持一层方法调用，不支持多层（一般很少会用到多层方法调用)，可以通过先bind一个变量调用一个方法，然后使用这个bind的这个值
2. 在写ignoreSql sql ${时 输入后看到代码提示时按enter会有一个不影响使用的报错，可以按tab替代，按tab不会报错
3. 有的用户不愿在代码中加入注释，这个问题以后再看，比如给一个配置文件来处理
