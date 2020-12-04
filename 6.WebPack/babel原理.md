## 什么是babel
- Babel 是一个 JavaScript 编译器。他把最新版的javascript编译成当下可以执行的版本，因为目前来说各个浏览器对es6的支持不太好，但是对es5比较友善，所以要让浏览器看的懂，就需要配一个“翻译官”，使得es6语法能让它们看得懂
### 引子
我们是怎么把英文翻译成自己看的懂得中文的呢？
- 用翻译英文she is cute举例

```
graph TB
she-is-cute-->主语
she-is-cute-->谓语
she-is-cute-->表语
主语-->人称代词
主语-->主语含义
主语含义-->她
谓语-->动词
谓语-->谓语含义
谓语含义-->is
表语-->形容词
表语-->表语含义
表语含义-->可爱
```

```
graph TB
she-is-cute-->主语
she-is-cute-->谓语
主语-->人称代词
主语-->主语含义
主语含义-->她
谓语-->动词
谓语-->谓语含义
谓语含义-->很可爱
```

## babel的工作流程
1. 解析parser
2. 转化transformer
3. 生成gernerater

### 解析
babel会把js代码进行解析生成AST（抽象语法树）
### 转换transformer
babel会通过生成的的AST对js代码中的es6语法进行转化成es5的AST
#### AST是什么？