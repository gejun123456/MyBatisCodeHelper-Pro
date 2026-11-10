
# 安装、试用与激活

## 先选择与你购买渠道对应的版本

| 购买渠道 | 安装版本 | 试用 / 购买入口 |
| --- | --- | --- |
| brucege.com 官网 | MyBatisCodeHelperPro，不带 Marketplace Edition | [官网试用与购买](https://brucege.com/pay/view) |
| JetBrains Marketplace；企业客户及中国以外用户 | MyBatisCodeHelperPro (Marketplace Edition) | [Marketplace](https://plugins.jetbrains.com/plugin/14522-mybatiscodehelperpro-marketplace-edition-) |

两个发行版本的购买和激活渠道不同。已有授权请安装对应版本；企业客户的购买与激活见 [企业客户说明](company.md)。价格、试用及授权条件以对应渠道页面为准。

安装后希望直接让 AI 调用插件，请继续 [安装并接入 AI](quickstart.md)。

## 安装
----

支持的 IDE 与兼容版本请以所安装发行版本的 Marketplace 页面为准。

- IntelliJ IDEA
- IntelliJ IDEA Community Edition
- Android Studio

**使用 IDE 内置插件系统:**
- <kbd>Settings / Preferences</kbd> > <kbd>Plugins</kbd> > <kbd>Marketplace</kbd> > 搜索上表中的对应插件名称 > <kbd>Install</kbd>

**直接下载** (不要解压zip 直接安装即可) 请根据IDEA的版本来下载对应的版本 
如果链接下载不了 可以加qq群 598080979 群文件里面有最新的版本
- download[`lastest plugin zip`](https://plugins.jetbrains.com/plugin/9837-mybatiscodehelperpro) -> <kbd>Preferences(Settings)</kbd> > <kbd>Plugins</kbd> > <kbd>Install plugin from disk...</kbd>


重启**IDE**.

### 安装后无法找到 Mapper 或 XML？

先等待项目索引完成，检查 XML namespace 与接口、模块依赖及资源目录。安装了多个 MyBatis 插件时，可能存在冲突，可先禁用其他相关插件并重启排查，详见 [常见问题](question.md)。


## 激活

以下激活码操作适用于官网购买的版本。Marketplace Edition 请按 [企业客户说明](company.md) 中的 JetBrains 账号 / 离线授权方式激活。

### 激活码激活  

- 未激活时IDEA打开项目时会有一个通知 在IDEA的eventLog可以找到 上面有一个一个register的按钮 点击按钮 输入激活码即可  
![register](https://images.brucege.com/register_new.gif)

- 或者可以在设置界面激活  
![](https://images.brucege.com//onlineActivation2.png)

网购购买的激活码请使用在线激活，无法联网的机器使用离线激活

在线激活码转离线激活码：https://brucege.com/keys ,生成了离线激活码后填入离线激活即可  

激活的时候 如果出现 connect error 请检查下IDEA是否设置了proxy 可以去掉proxy试试  

#### 如果还有问题，请参考 [激活问题排查](activate.md)


### 离线激活

- 由于激活的时候需要联网，某些公司可能设置了拦截，无法联网，此时可以先使用vpn或者手机开热点试试  
- 离线激活的教程参考下图，先购买在线激活码: http://brucege.com/pay/view

#### 请将离线激活里面的唯一码，还有购买的在线激活码发送给微信gejun12311,唯一码可以在idea设置 other mybatisCodeHelper拖最下面有个激活按钮找到
#### 走 https://brucege.com/keys 可以将线激活码转为离线激活码  
![offline](https://images.brucege.com/offlineActivateNew.png)
![weichaturl](https://images.brucege.com/wechatme.png)


## 查询激活码

- 网页 https://brucege.com/keys 可以通过邮箱来查询激活码  

## 解绑  

- 购买后会发两个激活码，可以在两台设备上绑定，一个激活码绑定一个设备。当更新机器或者重装系统时需要解绑。可进行下图的操作    
![unBind](https://images.brucege.com/unBind.png)
或者使用网页http://brucege.com/keys 来解绑
