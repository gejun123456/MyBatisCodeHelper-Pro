## if test when test
![If When Test Ognl Support](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/ifWhenTest中ognl支持.gif)

## bind And \${
![Bind And $ Ognl Support](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/bind和${的ognl支持.gif)


For $ statement, it can be anything, the sql cant be parsed, you can add a comment to make sql parseable, like this:

![AddSqlAfter$](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/add$sql.gif)

Or add a comment before the xml tag
![parse$byXmlTagComment](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/parse$byXmlTagComment.gif)


## foreach collection
![Collection Ognl Support](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/collection标签跳转检测正确.gif)

## ognl method call support and inspection
![ognl method call](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/collectionCallMethdo.gif)


## ognl single char string compare add toString call
![checkOgnlSingleCharStringCompare](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/checkOgnlSingleCharStringCompare.gif)


## Chained method calls and property access (3.7.0+)

In OGNL expressions such as `<if test="...">`, `<when test="...">`, and `<bind value="...">`, you can chain method calls and access properties between them. The plugin uses the type returned at each step to resolve the next member and provide completion and reference checks.

For example, in `user.getAddress().getCity().trim()`, `getCity()` returns a `String`, so completion after the next dot offers string methods such as `trim()`. You can also mix property access and method calls, as in `user.getAddress().city.trim()`.
