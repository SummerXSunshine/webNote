## nextTick

### 相关知识eventLopp

同步任务 >> 微任务 >> 宏任务

> https://jakearchibald.com/2015/tasks-microtasks-queues-and-schedules/

### 使用场景

nextTick我们常用来获取更新之后的dom，一般常用于对于更新之后的dom节点执行一些操作的时候去使用。

### 如何使用

1. vue组件中（.vue文件）中可以调用this.$nextTick(() => {}),来使用
2. 在vue的mounted之前的生命周期`beforecreated`, `created`和`beforemounted`中如果有对当前dom进行操作的时候必须使用`$nextTick`,因为这时候dom还没挂载上去。

### 怎么实现nextTick

#### 特殊情况：

执行vue内部的一些事件的时候的时候，比如v-on等情况会对nextTick中的回调进行一层`宏任务`的包裹，以下是这部分的源码。

```
/**
 * Wrap a function so that if any code inside triggers state change,
 * the changes are queued using a (macro) task instead of a microtask.
 */
 
export function withMacroTask (fn: Function): Function {
  return fn._withTask || (fn._withTask = function () {
    useMacroTask = true
    const res = fn.apply(null, arguments)
    useMacroTask = false
    return res
  })
}
```

### 总结

1. dom的更新是同步的（当然有些vue内部的涉及到状态改变的不是同步的，这种情况vue也做了处理。他会用一个宏任务包裹一下nextTick的回调）。
2. 渲染是异步的，dom同步更新我们看起来没有改变是因为UI渲染属于宏任务。
3. 因为dom改变是同步的，渲染是异步的，所以想通过$nexTick去实现某些页面变化的效果是不太可行的。
4. nextTick的兼容性MessageChannel > setImmediate > promise > mutationObserve > setTimout
5. 对于特殊的情况会对nextTick的回调进行`宏任务`的包裹