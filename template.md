



# 算法模版

## 树

### **树的遍历DFC**

```javascript
const transverse = (root) => {
  if (!root)return;
  // 前序遍历
  transverse(root.left);
  // 中序遍历
  transverse(root.right);
  // 后序遍历
}
```

### **层次遍历BFC**

```javascript
var levelOrder = function(root) {
    if(!root) return [];
    const stack = [];
    stack.push(root)
    const res = [];
    while(stack.length !== 0){
        const currentLevelSize = stack.length;
        res.push([]);
        for (let i = 1; i <= currentLevelSize; ++i) {
            const node = stack.shift();
            res[res.length - 1].push(node.val);
            if (node.left) stack.push(node.left);
            if (node.right) stack.push(node.right);
        }
    }
    return res;
};
```

### 有问题

```javascript
var buildTree = function(inorder, postorder) {
    if(!postorder.length) return null;
    const temp = postorder[postorder.length-1]; // 这一行有问题不知道为什么
    const node = new TreeNode();
    node.val = temp;
    const mid = inorder.indexOf(temp);
    node.left = buildTree(inorder.slice(0,mid),postorder.slice(0,mid));
    node.right = buildTree(inorder.slice(mid+1),postorder.slice(mid));
    return node;
};
```

### 二叉搜索
```javascript
var searchBST = function(root, val) {
    if(!root) return null;
    node = root;
    while(node){
        if(node.val === val){
            return node
        } else if(node.val < val){
            node = node.right;
        } else {
            node = node.left;
        }
    }
    return null;
};
```

### 逻辑计算

> leetcode461 https://leetcode-cn.com/problems/hamming-distance/

```

var hammingDistance = function(x, y) {
    let num = x ^ y;//得出一个所有位数上的值都不同的二进制值
    let res = 0;
    while (num) {
        res++;
        num &= num - 1 //计算所有位数上面1的个数
    }
    return res;
};
```

