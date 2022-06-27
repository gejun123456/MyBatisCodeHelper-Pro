## if test when test
![ifWhenTest中ognl支持](http://youpaiyuntupian.test.upcdn.net/ifWhenTest中ognl支持.gif)

## bind和 ${
![bind和${的ognl支持](http://youpaiyuntupian.test.upcdn.net/bind和${的ognl支持.gif)

对于 ${ 由于里面的输入可以是任意字符，sql会无法解析，插件引入了 $sql注释，如上图，真正要被替换的语句写入$sql 注释中

## foreach collection
![collection标签跳转检测正确](http://youpaiyuntupian.test.upcdn.net/collection标签跳转检测正确.gif)

## ognl中方法调用和检测
![ognl method call](http://youpaiyuntupian.test.upcdn.net/collectionCallMethdo.gif)

## ognl单字符串比较检测与提示添加toString调用
![checkOgnlSingleCharStringCompare](http://youpaiyuntupian.test.upcdn.net/checkOgnlSingleCharStringCompare.gif)

## 注意 
Ognl目前不支持多层方法的调用，如果有多层方法调用 请先bind一个变量 在调用下一个方法

类似于如下
![ognlbindcall](http://youpaiyuntupian.test.upcdn.net/ognlbindcall.png)
