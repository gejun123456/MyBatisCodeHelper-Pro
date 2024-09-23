## 插件支持mybatis注解
支持script标签，支持#{},if test,动态sql代码提示


### IDEA新版本会自动配置过java类@Select等的language injection配置，需要禁用掉，否则会导致在#{}中没有代码提示
![removeInjection](https://newimages.brucege.com/removeInjection.png)

### 使用注解需要先打开配置

![annotationSupport](https://newimages.brucege.com/annotationSupport.jpg)

### 支持注解的代码提示
![annotationHighlight](https://newimages.brucege.com/annotationHighlight.jpg)


## 不足

#### 注解的代码提示和检测没有xml那么好，复杂的sql能用xml还是建议用xml, 在注解上alt enter可以一键挪到xml中

### if test里面目前需要用单引号才有代码提示

## 用注解的可以加入注解交流群 qq群：725713937
