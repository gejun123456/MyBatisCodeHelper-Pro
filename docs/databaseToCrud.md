## 使用Intellij自带的datasource来生成 最简单的从数据库生成代码

![intellijDatasourceGenerateCrud](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/数据库生成和合并代码.gif)

选定了module后 插件会自动配置好java model folder, java mapper folder 以及 resource folder 一般不需要修改

只用第一次使用配置好包名就行了，包名有自动补全 2.0.1版本后插件会自动检测 generatedKey 一般不需要配置

在数据库添加了字段后 也可以重新生成，并且不会覆盖你的mapper接口中已经添加的方法

可生成service 生成到通用mapper及mybatisplus

## IDEA社区版可以使用添加的datasource来生成 （目前支持mysql oracle postgresql sqlserver  myql支持5.5及以上  oracle支持oracle10g及以上 postgresql sqlserver支持最新版，老版本未测试 有问题请联系我) 

![mybatis-database-generator](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/configDatabaseToUseMybatisGenerator.gif)

## 如何配置

一般只用配置下包名 就可以使用了
![mybatis-database-generator](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/DatabaseGenerateSetting.png)

## 使用mybatisGenerator的配置文件来生成(不推荐 直接从数据库生成更方便)

 mybatis generator 配置文件的规则   
  http://www.mybatis.org/generator/configreference/xmlconfig.html

![mybatis-generator](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/2017_08_06_mybatis_generator.gif)

## 一键生成mybatis generator的xml文件

![generate_mybatis_generator_config_file](https://raw.githubusercontent.com/gejun123456/MyBatisCodeHelper-Pro/master/screenshots/generate_mybatis_generator_config_file.gif)
