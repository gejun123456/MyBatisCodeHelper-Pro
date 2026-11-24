## if test when test

![ognlUseEnum](https://images.brucege.com/ognlUseEnum.png)

![ifWhenTest中ognl支持](https://images.brucege.com/ifWhenTest中ognl支持.gif)

## bind和 ${
![bind和${的ognl支持](https://images.brucege.com/bind和${的ognl支持.gif)

对于 ${ 由于里面的输入可以是任意字符，sql会无法解析，插件引入了 $sql注释，如下图，真正要被替换的语句写入$sql 注释中

![AddSqlAfter$](https://images.brucege.com/add$sql.gif)

或者在xml的标签上加一个$注释
![parse$byXmlTagComment](https://images.brucege.com/parse$byXmlTagComment.gif)

## foreach collection
![collection标签跳转检测正确](https://images.brucege.com/collection标签跳转检测正确.gif)

## ognl中方法调用和检测
![ognl method call](https://images.brucege.com/collectionCallMethdo.gif)

## ognl单字符串比较检测与提示添加toString调用
![checkOgnlSingleCharStringCompare](https://images.brucege.com/checkOgnlSingleCharStringCompare.gif)

## 链式方法调用与属性访问（3.7.0 起）

在 `<if test="...">`、`<when test="...">` 和 `<bind value="...">` 等 OGNL 表达式中，可以连续调用方法，也可以在方法调用之间访问属性。插件使用每一步的返回类型解析下一步，并提供补全和引用检查。

例如，`user.getAddress().getCity().trim()` 中，`getCity()` 返回 `String`，因此输入下一个 `.` 后会看到 `trim()` 等字符串方法。也可以混用属性与方法，例如 `user.getAddress().city.trim()`。
