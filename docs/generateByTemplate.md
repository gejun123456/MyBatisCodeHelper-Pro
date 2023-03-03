## 迁移到模版来生成代码（插件3.1.8版本，即将发布）

### 部分用户用定制的需求，推荐用模版来生成代码

### MybatisCodeHelperPro插件为3.1.8或以上的版本，安装EasyCodeMybatisCodeHelper插件来进行模版生成

### 提供了一个模版商城 https://brucege.com/easyCodePage 或者到 https://github.com/gejun123456/MybatisCodeHelperTemplates 下载模版

从模版商城下载模版后，通过json导入到EasyCodeMybatisCodeHelper插件中  

global config选择为MybatisCodeHelperPro, template选择为MybatisCodeHelperMigrate

然后修改模版global config, mybatisCodeHelper.vm的配置，将mybatis generator的配置迁移到模版中

可以从IDEA数据库表上右键Mybatis generator下面迁移到模版生成，把生成的路径等信息拷出来到MybatisCodeHelper.vm那里生成即可
![projectTemplateInfo](https://images.brucege.com/projectTemplateInfo.png)

![mybatisCodeHelper.vm](https://images.brucege.com/easyCodeMybatisCodeHelperGlobalConfig.png)

建议每个生成配置的global config copy一下改成当前项目的名字，比如MybatisCodeHelperPro-DemoProject这种

使用IDEA社区版的可以加qq群516959916，里面有社区版可用的模版插件

未来将提供更多模版，欢迎大家提供模版，使用模版碰到问题可以联系我


