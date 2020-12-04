## 事件循环

### 同步任务


### 异步任务
不是同步执行的代码都会放到异步任务队列中，而异步任务又分为宏任务和微任务


#### 宏任务

**常见的的宏任务**
# | 浏览器 | node
---|--- | ---
setTimeout | yes | yes
setInterval | yes | yes
setImmediate | no | yes
requestAnimationFrame|yes|no

**常见的微任务**
# | 浏览器 | node
---|--- | ---
process.nextTick | no | yes
MutationObserve | yes | no
promise .then .catch .finally|yes|yes







#### 微任务

常见的微任务有promise

### 例子

### 总结
> 执行顺序: 同步任务>>微任务>>宏任务