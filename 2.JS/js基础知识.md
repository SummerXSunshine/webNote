## js基础

### 1-数组扁平化
将一个多维数组转化成一维数组

- 使用flat方法

```javascript
const arr = [1, 2, 3, [4, 5, 6]]
arr.flat();
// arr => [1, 2, 3, 4, 5, 6]
```

- 使用正则

```javascript
const arr = [1, 2, 3, [4, 5, 6]]
const res = JSON.stringify(arr).replace(/\[|\]/g, '').split(',');
// 数据都会变成string类型
```

### 2-数组去重

```javascript

```