## Vue

### 特点
1. 数据响应式
2. 双向绑定
3. 观察者订阅者模式

### 数据响应式

#### Vue2

通过defineProperty实现数据劫持给每个属性设置getter和setter，数据的每一个更改都会被感知到，从而实现数据响应的目的
#### Vue3.0

通过proxy来代替defineProperty，相比Vue2中的defineProperty性能更好，性能优化是浏览器去实现的。

**实现代码**
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Proxy</title>
</head>
<body>
<div id="app">hello</div>

<script>
  let data = {
    msg: 'hello world',
    count: 0,
  }
  let vm = new Proxy(data, {
    get(target, key){
      console.log('get: key', key, target[key])
      return target[key]
    },
    set(target,key, newValue){
      if ( target[key]=== newValue){
        return;
      }
      target[key] = newValue;
      console.log('set:target', newValue)
      document.querySelector('#app').textContent = target[key];
    }
  })
  
  // 测试样例
  vm.msg = 'good';
  console.log(vm.msg);
</script>
</body>
</html>

```


