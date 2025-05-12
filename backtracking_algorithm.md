# 框架
```
result = []
def backtrack(路径, 选择列表):
    if 满足结束条件:
        result.add(路径)
        return
    
    for 选择 in 选择列表:
        # 做选择  即多叉树的前序位置
        将该选择从选择列表移除
        路径.add(选择)
        backtrack(路径, 选择列表)
        # 撤销选择 即多叉树的后续位置
        路径.remove(选择)
        将该选择再加入选择列表
```

[全排列问题](https://leetcode.com/problems/permutations/description/)
```
# 例子 数字的全排列算法： 输入一组不重复的数组，返回其全排列

class Solution:
    def __init__(self):
        # 记录全路径结果
        self.res = []

    def permute(self, nums):
        # 记录路径
        track = []

        # 记录是否出现
        used = [False] * len(nums)
        self.backtrack(nums, track, used)

        return self.res

    def backtrack(nums, track, used):
        if len(track) == len(nums):
            self.res.append(track.copy())
            return
        for i in range(len(nums)):
            # 已经被使用过
            if used[i]:
              continue
            # 做选择
            track.append(nums[i])
            used[i] = True
            self.backtrack(nums, track, used)
            # 进入下一层决策树
            # 取消选择
            track.pop()
            used[i] = False
            
             
```
