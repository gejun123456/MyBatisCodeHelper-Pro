## mybatis接口方法名重构支持
![renameMapperMethod](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/renameMapperMethod.gif)

## mybatis param的自动补全
![paramComplete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/paramComplete.gif)

## mybatis param检测是否正确
![检测param是否正确](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/检测param是否正确.gif)

## resultMap refid 跳转到定义和重构

![resultMap](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/resultMapJump.gif)

## property refid resultMap等的自动补全

![property complete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/propertyComplete.gif)

## resultMap中的collection association自动补全

![associactionAndCollectionComplete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/associationAndCollectionCouldAutoComplete.gif)

## xml中if test的自动补全
![iftestCompltete](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/ifTestCompletion.gif)

## 任意位置的sql的自动补全 识别include trim where set 等mybatis的标签

对于Intellij的数据库来说 可以对一个xml的标签 注入sql语法
补全的时候由于不能识别mybatis的这些标签，导致在写了上述的标签后 之后的sql无法进行自动补全
插件优化了这块，可以让Intellij正确识别这些标签 正确解析sql语法

trim标签
![trim标签正确性检测](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/trim标签正确性检测.gif)

set标签
![set标签正确性](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/set标签正确性.gif)

解析sql的正确性 需要先配置下

![databaseConfig](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/configDatabase.png)





