## AST

### 基本介绍

### 使用场景

### 

#### 节点类型

- FunctionDeclaration-自定义函数声明节点

- Identifier-自定义标识符节点

- blockStatement-自定义块语句节点

- ReturnStatement-自定义返回语句节点

- BinaryExpression-自定义二进制表达式节点

- variableDeclaration-自定义变量声明节点

- variableDeclarator-自定义变量声明符节点

- functionExpression-自定义函数表达式节点

  ```javascript
  var test = function sum(a,b){return a+b}	
  ```

### 实例

#### ==换成===

#### 箭头函数转换

#### 依赖

```json
{
  "name": "AST",
  "version": "1.0.0",
  "dependencies": {
    "escodegen": "^2.0.0",
    "esprima": "^4.0.1",
    "estraverse": "^5.2.0"
  }
}

```

