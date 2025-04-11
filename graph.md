# 图的基础结构
## 图的逻辑结构
```
class Graph：
  def __init__(self, val):
    self.val = val
    self.neighbors = []
```

## 图的存储方式
```
# 邻接表
# graph[x] 存储x的所有邻居节点
graph: List[List[int]] = []

# 邻接矩阵
# matrix[x][y] 记录是否有一条边从x指向y
matrix: List[List[Bool]] = []

# 如果图的节点不是int 就用一个哈希表映射一下就可以
```

```
# 带权重的图存储
# 邻接表
# graph[x] 存储 x 的所有邻居节点以及对应的权重
# 具体实现不一定非得这样，可以参考后面的通用实现
class Edge:
    def __init__(self, to: int, weight: int):
        self.to = to
        self.weight = weight

graph: list[list[Edge]] = []

# 邻接矩阵
# matrix[x][y] 记录 x 指向 y 的边的权重，0 表示不相邻
matrix: list[list[int]] = []
```


# DFS 深度优先遍历
**DFS 算法求所有路径**

1. Onpath: onpath用于寻找路径，记录路径是否被访问. 从初始节点到目标节点：寻找所有路径，访问到目标节点则退出在后序位置进行**pop**，再寻找新的路径
2. Visited: 用于记录节点是否被访问过
3. **两种方法都是在图有环的时候使用的结构，如果没有环其实用不到**
4. 普通无环情况下 使用path记录路径即可

# BFS 广度优先遍历

1. BFS 算法一般只用来**寻找那条最短路径，不会用来求所有路径**
