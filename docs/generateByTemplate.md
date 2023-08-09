## 迁移到模版来生成代码（插件3.1.9版本）

### 部分用户有定制的需求，比如公司代码要加特定的注释等，或者用了公司内部框架等，推荐用模版来生成代码

### MybatisCodeHelperPro插件为3.1.9或以上的版本，安装EasyCodeMybatisCodeHelper(1.3.0)版本插件来进行模版生成

### 支持写模版代码提示，实时预览模版，直接在idea编辑器操作模版，可配置多个分组，最方便的模版生成代码插件

视频地址: https://www.bilibili.com/video/BV1dL41127SQ  

github:https://github.com/gejun123456/EasyCodeMybatisCodeHelperTemplates 下载模版文件
直接把模版文件拷到项目的easyCode目录或者Scratches And Consoles的/extensions/EasyCode到来生成代码，写模版有代码提示，可以实时预览模版，直接在idea编辑器操作模版 

或者可以从json导入老模版   
![importToScratch](https://images.brucege.com/importToScratch.png)

模版预览:    
![scratchGenerate](https://images.brucege.com/scrachGenerate.gif)

生成代码,在idea的数据库表上,可以选多张表生成:
![generateFromScratch](https://images.brucege.com/generateFromScratch.png)

目前支持项目的easyCode目录或者scratch目录下的/extensions/EasyCode目录进行识别生成代码

推荐使用项目的easyCode目录，可以放到git中以及和同事共享防止丢失

## 怎么从之前设置配置的模版导入到 从easycode文件目录生成代码
先将之前设置配置的导入到json，再从json导入到scratch那个，导入到scratch后 就可以直接复制easyCode文件夹到项目的根目录，
弄一个group.json就可以生成代码了


## 我不会写模版怎么办？
模版用的是velocity语法 文档:https://velocity.apache.org/ 碰到模版问题也可联系我来弄弄

### 升级插件注意
由于1.2.8版本对存储进行了更改，从1.2.7版本之前升级到之后的版本，需要先导出模版到json，升级到高版本然后导入json.

### 模版生成的代码column连在了一起，中间没有逗号
2023.1 idea升级了velocity，把$velocityHasNext 改成$foreach.hasNext即可

### projectPath为空
如果你的项目是一个多module平行的项目，没有一个总的project，可以在mybatisCodehelper.vm中将projectPath set为具体的路径  
#set($projectPath="D:/workspace/idea/XXModule")

### GenerateCode(old)和GenerateFromEasyCodeFolder(new)的区别是啥
GenerateCode(old)老的模版是在设置里面配置的,走的是设置里面的template globalConfig等配置,  
GenerateFromEasyCodeFolder(new)是直接从easyCode文件夹下的模版生成的.
当你使用GenerateFromEasyCodeFolder(new) 无需在设置里面配置模版，推荐使用GenerateFromEasyCodeFolder(new),  
写模版有代码提示，可以实时预览模版，直接在idea编辑器操作模版，还可以加到git中方便与同事共享


### EasyCodeMybatisCodeHelper插件代码fork自 https://github.com/makejavas/EasyCode 插件，修改了部分代码用于兼容MybatisCodeHelperPro插件



