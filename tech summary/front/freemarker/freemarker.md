# 记录freemarker相关知识点 #

## list ##

1. 首先判定list是否存在并且不为空
`<#list xxlist?? && xxlist?size gt 0 >`
2. list下标，只需要在元素后面添加_index  `<#list xxlist as item> ${item_index + 1}` 
3. 