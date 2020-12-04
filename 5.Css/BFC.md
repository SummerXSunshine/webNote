## 什么是BFC
- blick formating contex块级格式化上下文

### 定义
决定元素如何对它进行定位以及其它元素的相关关系和相互作用，总觉来说就是让元素脱离文档流。
### 如何触发BFC
1. floa不为none
2. position为absolute，fixed或者sticky
3. overflow为auto， hidden， scroll
4. display的值位table-cell或者inline-block



### 解决问题
####    解决自适应变化的问题

### 效果
- 触发BFC脱离文档流不会影响其他元素
- 