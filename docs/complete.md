## mybatis param的自动补全
![betterParamAutoComplete](https://images.brucege.com/betterParamAutoComplete.gif)

## mybatis param检测是否正确
![检测param是否正确](https://images.brucege.com/检测param是否正确.gif)

## property refid resultMap等的自动补全
![autoCompleteForPropertyResultMapEct](https://images.brucege.com/autoCompleteForPropertyResultMapEct.gif)


## 任意位置的sql的自动补全 识别include trim where set 等mybatis的标签
对于Intellij的数据库来说 可以对一个xml的标签 注入sql语法
补全的时候由于不能识别mybatis的这些标签，导致在写了上述的标签后 之后的sql无法进行自动补全
插件优化了这块，可以让Intellij正确识别这些标签 正确解析sql语法

trim标签
![trim标签正确性检测](https://images.brucege.com/trim标签正确性检测.gif)

set标签
![set标签正确性](https://images.brucege.com/set标签正确性.gif)

解析sql的正确性 需要先配置下

![databaseConfig](https://images.brucege.com/configDatabase.png)





