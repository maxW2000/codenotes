# 二叉树的思维模式
1. **是否可以通过遍历一遍二叉树得到答案**？如果可以，用一个 traverse 函数配合外部变量来实现，这叫「遍历」的思维模式。
2. **是否可以定义一个递归函数，通过子问题（子树）的答案推导出原问题的答案**？如果可以，写出这个递归函数的定义，并充分利用这个函数的返回值，这叫「分解问题」的思维模式。
无论哪种思维模式都需要：如果单独抽出一个二叉树节点，**它需要做什么事情**？**需要在什么时候（前/中/后序位置）做**？其他的节点不用你操心，递归函数会帮你在所有节点上执行相同的操作

# 前序 中序 后序的本质
所谓**前序位置**，就是刚进入一个节点（元素）的时候，**后序位置**就是即将离开一个节点（元素）的时候 <br>
前中后序是遍历二叉树过程中处理**每一个节点的三个特殊时间点**
1. 前序位置的代码在**刚刚进入**一个二叉树节点的时候执行； **只能从函数参数中获取父节点传递来的数据**。
2. 后序位置的代码在**将要离开**一个二叉树节点的时候执行；**不仅可以获取参数数据，还可以获取到左子树**通过函数返回值传递回来的数据
3. 中序位置的代码在一个二叉树节点**左子树都遍历完，即将开始遍历右子树**的时候执行。**最强**不仅可以获取参数数据，还可以同时获取到左右子树通过函数返回值传递回来的数据

**需要去思考遍历的时候 什么操作需要放在什么位置 前序，中序，还是后序**

# 二叉树 构造篇
**二叉树的构造问题一般都是使用「分解问题」的思路：构造整棵树 = 根节点 + 构造左子树 + 构造右子树。**
1. [前序中序构建二叉树](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/description/)
2. [后序中序构建二叉树](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/description/)
3. [前序后序构架二叉树](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/description/)


# 二叉树 题目练习

## 递归 遍历思维模式
题库 -> (https://labuladong.online/algo/problem-set/binary-tree-traverse-i/) <br>
题库2 -> https://labuladong.online/algo/problem-set/binary-tree-traverse-ii/


```
#跟路径有关的题目模板都是
def targetfunction(root):
  self.path = [] / "" 字符串或者列表
  self.traverse(root)
  # 根据题目需要定义
  self.res
  self.sum / count 等
  self.depth

def traverse(root):
  if root is None:
    return

  # 根据题目对叶子节点进行判断并且修改参数 self.path 等
  if root.left is None and root.right is None:
      一系列判断
      return

  self.path 更新
  # 前序位置

  # 根据题目要求 判断先right 还是 left
  self.traverse(root.left)
  self.traverse(root.right)

  # 后序位置
  self.path 退出
  
```
## 递归 分解问题思维模式

## 非递归 层序遍历
