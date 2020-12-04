## 闭包
闭包的用处：
     ①.读取函数变量
     ②.让这些变量的值始终存在内存中。由于闭包会携带包含它的函数的作用域，因此会比其他函数占用更多的内存。过度使用闭包可能会导致内存占用过多，因此要慎重使用

闭包的创建

```
function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n); 
　　　　}
　　　　return f2;
　　}
　　var result=f1();
　　result();    // 999
　　
　　// 推荐写法
　　(function(window) {
　　　　var n=999;
　　　　return {
　　　　    f2(){
　　　　　　    alert(n); 
　　　　}
　　　　};
　　})(window)
　　var result=f1();
　　result();    // 999
　　
　　// 推荐写法
```

### this指向

```
var name = "the window";

var object = {
    nama: "my object",
    
    getNameFunc : function() {
        return function() {
            return this.name;
        }
    }
};
alert(object.getNameFunc()());    //"the window"(非严格模式)
```

## 模块模式
感觉模块化就是利用了匿名函数实现了块级作用域,在函数内定义的变量不会被外界访问,然后如果说有公共的变量直接通过return的方式返回内部的变量到外部。
```
var application = function() {
    //私有变量
    var components = new Array();
    //初始化
    components.push(new BaseComponents());
    //公共
    return {
        if(typeof components == "object"){
            components.push(components);
        }
    }
    
}
```

