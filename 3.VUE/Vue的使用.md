## create
## watch
### 立即执行
利用watch的immediate和handle属性简写
```
watch: {
    {
        test: {
          handler(val, oldVal) {
            console.log("数据变化");
          } // 和普通的function没啥区别
        },
        immediate: true; // 会监听第一次变化
    }
}
```