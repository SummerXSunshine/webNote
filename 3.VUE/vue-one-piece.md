# Vue3.0

1. 放弃数据响应式的方式，同时兼容性变差
2. 全面支持typescript
3. 重写了虚拟dom
4. 观察者更加准确
5. virtual dom完全重写，mounting和patching提速100%

## 数据响应式

### Vue2

通过defineProperty实现数据劫持给每个属性设置getter和setter，数据的每一个更改都会被感知到，从而实现数据响应的目的
### Vue3.0

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





## setup（）方法

> 类似于react中的hook，基本上是从react中借鉴过来的



### 访问组件的 property

执行 `setup` 时，组件实例尚未被创建。因此，你只能访问以下 property：

- `props`
- `attrs`
- `slots`
- `emit`

换句话说，你**将无法访问**以下组件选项：

- `data`
- `computed`
- `methods`

## 体积优化

去除vue.prototype的写法，模块化了，应用`tree shaking`来使打包的体积更小



## virtual dom重写

1. 静态节点比如说一个常量标签`<div>Vue3.0</div>`这种节点会被打上标记，在updatechildren()的时候会直接跳过这种节点





## 路由

1. 安装：`npm install vue-router@4`

2. 路由配置变化：

   原来：

   ```js
   import Router from 'vue-router';
   import Dialog from '@/views/Dialog';
   import Admin from '@/views/Admin';
   
   Vue.use(Router);
   
   export default new Router({
     routes: [{
       path: '/',
       name: 'dialog',
       component: Dialog,
     }, {
       path: '/admin',
       name: 'admin',
       component: Admin 
     }]
   })
   ```

   

   现在:

   ```js
   import { createRouter, createWebHashHistory } from 'vue-router';
   import Admin from '../views/Admin';
   import Dialog from '../views/Dialog/index.vue';
   
   const routerHistory = createWebHashHistory()
   
   export default createRouter({
     history: routerHistory,
     routes: [{
       path: '/',
       name: 'dialog',
       component: Dialog 
     }, {
       path: '/admin',
       name: 'admin',
       component: Admin
     }]
   })
   
   ```

3. 获取路由方式

   1. `Option API`中获取和`vue2`中的方式是一样的

   2. `Composition API`:

      ```js
      import { useRouter, useRoute } from 'vue-route';
      
      export default {
        setup(() => {
          const router = useRouter();
          const route = useRoute();
      	})
      }
      
      
      ```

      