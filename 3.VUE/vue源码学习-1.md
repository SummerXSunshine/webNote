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

#### Proxy和Object.defineProperty的区别

Proxy 的意思是代理，我一般叫他拦截器，可以拦截对象上的一个操作。用法如下，通过 new 的方式创建对象，第一个参数是被拦截的对象，第二个参数是对象操作的描述。实例化后返回一个新的对象，当我们对这个新的对象进行操作时就会调用我们描述中对应的方法。

```javascript
new Proxy(target, {
    get(target, property) {

    },
    set(target, property) {

    },
    deleteProperty(target, property) {

    }
})
```

Proxy和Object.defineProperty的区别

- Object.defineProperty只能监听到属性的读写， 而Proxy除了读写外还可以监听属性的删除，方法的调用等。
- 我们想要监视数组的变化，基本要依靠重写数组方法的方式实现，这也是 Vue 的实现方式，而 Proxy 可以直接监视数组的变化。
```javascript
const list = [1, 2, 3];
const listproxy = new Proxy(list, {
   set(target, property, value) {
       target[property] = value;
       return true; // 标识设置成功
   }
});
list.push(4);
```
- Proxy 是以非入侵的方式监管了对象的读写，而 defineProperty 需要按特定的方式定义对象的属性。

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


