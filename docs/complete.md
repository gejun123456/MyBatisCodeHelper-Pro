## mybatis接口方法名重构支持

![refacterMethodName](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/refactor_method_name.gif)

## mybatis param的自动补全

![autocomplete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/simplecompletion.gif)

## resultMap refid 跳转到定义和重构

![resultMap](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/resultMapJump.gif)

## property refid resultMap等的自动补全

![property complete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/propertyComplete.gif)

## collection的自动补全

![collection complete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/listRecommeds.gif)


## resultMap中的collection association自动补全

![associactionAndCollectionComplete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/associationAndCollectionCouldAutoComplete.gif)

## xml中if test的自动补全
![iftestCompltete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/ifTestCompletion.gif)

## 任意位置的sql的自动补全 识别include trim where set 等mybatis的标签

对于Intellij的数据库来说 可以对一个xml的标签 注入sql语法
补全的时候由于不能识别mybatis的这些标签，导致在写了上述的标签后 之后的sql无法进行自动补全
插件优化了这块，可以让Intellij正确识别这些标签 正确解析sql语法

![trimAndSet](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/tirmAndSetDetect.gif)

![where](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/whereAutoCompleteAndSqlDetectInTag.gif)






