## 什么是promises
- https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Promise
- Promise 对象是一个代理对象（代理一个值），被代理的值在Promise对象创建时可能是未知的。它允许你为异步操作的成功和失败分别绑定相应的处理方法（handlers）。 这让异步方法可以像同步方法那样返回值，但并不是立即返回最终执行结果，而是一个能代表未来出现的结果的promise对象。
有回应的异步方法。

### 三种状态
同一个promise的状态只能从pendding->resolved或者pendding->rejected.

1. pendding 正在进行操作
2. rejected 操作失败
3. resolved 操作完成

### 基本api
- Promise.resole()
- Promise.reject()
- Promise.prototype.then()
- Promise.prototype.catch()
- Promise.all() // 所有的都完成之后
- Promise.race() // 其中有一个完成就执行

### 用法
#### 1-代码立即执行
```javascript
var p = new Promise((resolve,reject)=>{
    console.log("create successful");
    resolve("fullfill successful")
})

console.log("after new Promise");

p.then((value) =>{
    console.log(value);
})
```
输出结果
1. create successful
2. after new Promise
3. fullfill successful

#### 2-状态不可逆
同一个promise的状态只能从pendding->resolved或者pendding->rejected.
```javascript
var p1 = new Promise((resolve, reject)=>{
    resolve("success1");
    resolve("success2");
});

var p2 = new Promise((resolve, reject)=>{
    resolve("success");
    reject("reject");
});

p1.then((value)=>{
    console.log(value);
});

p2.then((value)=>{
    console.log(value);
});
```
输出结果
1. success1
2. success

#### 3-回调异步性
```javascript
var p = new Promise((resolve, reject)=>{
  resolve("success");
});

p.then((value)=>{
  console.log(value);
});

console.log("which one is called first ?");

```
输出结果
1. which one is called first ?
2. success


#### 4-获取promise返回的value值
- await获取
- then获取

```javascript

// 1.await 获取promise的返回值
async getValue {
    const value = await Promise;
    return value;
}
// 2.使用.then方法去获取
function getValue {
    let res;
    promise.then((value) => {
        res = value;
    })
    return res;
}

```