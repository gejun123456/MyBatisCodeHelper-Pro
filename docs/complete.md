## mybatis param的自动补全
![betterParamAutoComplete](http://youpaiyuntupian.test.upcdn.net/betterParamAutoComplete.gif)

## mybatis param检测是否正确
![检测param是否正确](http://youpaiyuntupian.test.upcdn.net/检测param是否正确.gif)

## property refid resultMap等的自动补全
![autoCompleteForPropertyResultMapEct](http://youpaiyuntupian.test.upcdn.net/autoCompleteForPropertyResultMapEct.gif)

## resultMap column 检测是否正确(2.7.2)
![resultMapColumnInspectionAndAutoComplete](http://youpaiyuntupian.test.upcdn.net/resultMapColumnInspectionAndAutoComplete.gif)

## resultMap中的collection association自动补全
![resultMapCollectionAndAssociactionBetterAutoComplete](http://youpaiyuntupian.test.upcdn.net/resultMapCollectionAndAssociactionBetterAutoComplete.gif)

## 任意位置的sql的自动补全 识别include trim where set 等mybatis的标签
对于Intellij的数据库来说 可以对一个xml的标签 注入sql语法
补全的时候由于不能识别mybatis的这些标签，导致在写了上述的标签后 之后的sql无法进行自动补全
插件优化了这块，可以让Intellij正确识别这些标签 正确解析sql语法

trim标签
![trim标签正确性检测](http://youpaiyuntupian.test.upcdn.net/trim标签正确性检测.gif)

set标签
![set标签正确性](http://youpaiyuntupian.test.upcdn.net/set标签正确性.gif)

解析sql的正确性 需要先配置下

![databaseConfig](http://youpaiyuntupian.test.upcdn.net/configDatabase.png)





