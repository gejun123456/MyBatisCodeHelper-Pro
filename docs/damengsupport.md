# 达梦数据库支持 (xml中sql自动提示和补全)

达梦数据库语法类似于oracle,

参考文章 https://blog.csdn.net/ilqgffvramusm2864/article/details/106211496

## 新方法(推荐)
使用官方的驱动  
然后在驱动的options中配置dialect为oracle   
![damengDialect](https://images.brucege.com/damengdialect.png)

然后可以配置resolutionScope到对应的数据库上:  
![resolutionScopedamgn](https://images.brucege.com/damengResolutionScope.png)

sqlDialect也设置为oracle  

最后的结果:表名和字段名会有代码提示,不再标红,可以识别oracle的函数  

当然部分达梦非oracle的语法无法识别会标红,这个是由于intellij不支持达梦导致的  

![damgnresult](https://images.brucege.com/damengFinalResult.png)

## 老方法 部分不能识别

设置中dialect配置 oracle 参考文档配置数据库那节

上面文章中的驱动 需要改为我改过的驱动 idea会把达梦数据库识别为oracle数据库。
兼容的是oracle的语法，达梦数据库支持的非oracle语法则不能识别。  

驱动下载地址:https://share.weiyun.com/mdyhnTtL

如果急用，请把方言配置为generic sql 然后使用官方的驱动,注意这个方法sql代码提示很少，sql会标红等
官方驱动下载地址:https://eco.dameng.com/download/

## 如果实在用不了 复杂的方法

本地弄一个 oracle，把达梦的表使用DTS工具迁移过去，然后在 oracle 的表上操作

## idea社区版 达梦数据库生成

请加入qq群516959916 里面单独支持社区版的版本

