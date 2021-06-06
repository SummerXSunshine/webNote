# Mini-webpack

webpack的功能很强大，这里实现一个简单的webpack

> demo: https://github.com/SummerXSunshine/mini-webpack

## TODO

首先了解一下实现一个mini-webpack做了些什么？

  1. 从入口文件开始，分析整个应用的依赖树
  2. 将每个依赖模块包装起来，放到一个数组中等待调用
  3. 实现模块加载的方法，并把它放到模块执行的环境中，确认模块间可以互相调用
  4. 把执行入口文件的罗技放在一个函数表达式中，并立即执行这个函数

## 准备工作

接下来准备一些已经封装好的库去完成上面的TODO

```
npm install @babel/core @babel/parser @babel/preset-env @babel/traverse --save-dev
```



1. `@babel/parser`: 分析我们通过 fs.readFileSync 读取的文件内容，返回 AST (抽象语法树)
2. `@babel/traverse`: 可以遍历 AST, 拿到必要的数据
3. `@babel/core`: babel 核心模块，其有个transformFromAst方法，可以将 AST 转化为浏览器可以运行的代码
4. `@babel/preset-env`: 将代码转化成 ES5 代码

## 实现步骤

## 1. 生成依赖

```
function createAsset(filename) {
  // 读取文件内容
  const content = fs.readFileSync(filename, 'utf-8')
  // 使用 @babel/parser（JavaScript解析器）解析代码，生成 ast（抽象语法树）
  const ast = babelParser.parse(content, {
    sourceType: "module"
  })

function createGraph(entry) {
  // 从入口文件开始，解析每一个依赖资源，并将其一次放入队列中
  const mainAssert = createAsset(entry)
  const queue = {
    [entry]: mainAssert
  }
  
```

## 2. 打包

```
const graph = createGraph(entry)
function bundle(graph) {
  let modules = ''
  for (let filename in graph) {
    let mod = graph[filename]
    modules += `'${filename}': [
      function(require, module, exports) {
        ${mod.code}
      },
      ${JSON.stringify(mod.mapping)},
    ],`
  }
```

