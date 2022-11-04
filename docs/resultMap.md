## 自动匹配resultMap中的字段
autoMap会找到resultMap type中的属性与resultMap引用的sql select的字段以最近的字段来进行匹配
![automap](https://myimages.brucege.com/automap.png)

支持columnPrefix匹配
![joinAutoMapping](https://myimages.brucege.com/joinAutoMapping.gif)

## check result column 检测select语句中有但是resultMap中没有的column 批量生成好匹配
![checkResultColumn](https://myimages.brucege.com/checkResultMapColumns.gif)

## 检测resultMap中重复的column
![checkDuplicateColumn](https://myimages.brucege.com/checkDuplicateColumn.png)


## resultMap column and property 自动提示和检测
![resultMapColumnPropertyAutoComplete](https://myimages.brucege.com/resultMapColumnPropertyAutoComplete.gif)

### resultMap column 检测是否正确(2.7.2)
![resultMapColumnInspectionAndAutoComplete](https://myimages.brucege.com/resultMapColumnInspectionAndAutoComplete.gif)

### resultMap中的collection association自动补全
![resultMapCollectionAndAssociactionBetterAutoComplete](https://myimages.brucege.com/resultMapCollectionAndAssociactionBetterAutoComplete.gif)

## 将resultType转换为resultMap
![convertResultTypeToResultMap](https://myimages.brucege.com/convertResutlTypeToResultMap.png)
