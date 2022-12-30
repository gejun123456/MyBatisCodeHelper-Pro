## if test when test

![ognlUseEnum](https://myimages.brucege.com/ognlUseEnum.png)

![ifWhenTest中ognl支持](https://myimages.brucege.com/ifWhenTest中ognl支持.gif)

## bind和 ${
![bind和${的ognl支持](https://myimages.brucege.com/bind和${的ognl支持.gif)

对于 ${ 由于里面的输入可以是任意字符，sql会无法解析，插件引入了 $sql注释，如下图，真正要被替换的语句写入$sql 注释中

![AddSqlAfter$](https://myimages.brucege.com/add$sql.gif)

或者在xml的标签上加一个$注释
![parse$byXmlTagComment](https://myimages.brucege.com/parse$byXmlTagComment.gif)

## foreach collection
![collection标签跳转检测正确](https://myimages.brucege.com/collection标签跳转检测正确.gif)

## ognl中方法调用和检测
![ognl method call](https://myimages.brucege.com/collectionCallMethdo.gif)

## ognl单字符串比较检测与提示添加toString调用
![checkOgnlSingleCharStringCompare](https://myimages.brucege.com/checkOgnlSingleCharStringCompare.gif)

## 注意 
Ognl目前不支持多层方法的调用，如果有多层方法调用 请先bind一个变量 在调用下一个方法

类似于如下
![ognlbindcall](https://myimages.brucege.com/ognlbindcall.png)
