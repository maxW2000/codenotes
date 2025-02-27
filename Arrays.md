# 双指针技巧

## 左右指针 从最左和最右
[167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

不需要考虑相对位置 如果考虑就需要用快慢指针 参考283. movezero
[27. Remove Element](https://leetcode.com/problems/remove-element/description/)

[344. Reverse String](https://leetcode.com/problems/reverse-string/description/)

[LCR 006. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/kLl5u1/description/)
[11. 盛最多水的容器](https://leetcode.cn/problems/container-with-most-water/)

## 快慢指针
一般都有一个快指针负责探路判断 慢指针负责处理结果 随后再增加
[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)

[83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

## 中心扩散指针
以每个元素为中心进行中心扩散去寻找回文串，并记录当前回文串的长度
[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

## 滑动窗口 
- **本质也是双指针 一快一慢  但是需要去维护这个窗口**
- **思考什么时候缩小窗口 什么时候更新窗口，条件是什么**
- **windows**一般就是包含满足条件的字符 找子串
- **need**是题目要求的子串的字典 字符:个数 需要初始化给予
- O(N)复杂度，在于**如何聪明的穷举**
```
# 滑动窗口算法伪码框架
def slidingWindow(s: str):
    # 用合适的数据结构记录窗口中的数据，根据具体场景变通
    # 比如说，我想记录窗口中元素出现的次数，就用 map
    # 如果我想记录窗口中的元素和，就可以只用一个 int
    window = ...
    need = ... #可选 取决于题目是否有安排字串的匹配需求
    """ window[c] = window.get(c,0) + 1
        get操作可以如果有c 就返回c的value 没有就返回0 所以更好用
    """

    left, right = 0, 0
    #也可能有valid = 0 一般看题目的子串要求
    #valid 是出现字符数相等时才更新的 比如need有2个a 所以window也得有2个a才会++
    #这样只需要比较valid与need的长度匹配 那就说明当前窗口与字串要求（具体要求需要自己更改去写）是匹配的 因为不需要管顺序

    while right < len(s):
        # c 是将移入窗口的字符
        c = s[right]
        # 增大窗口
        right += 1
        # 进行窗口内数据的一系列更新
        # 有条件的去
        window.add(c)
        ...

        # *** debug 输出的位置 ***
        # 注意在最终的解法代码中不要 print
        # 因为 IO 操作很耗时，可能导致超时
        # print(f"window: [{left}, {right})")
        # ***********************

        # 判断左侧窗口是否要收缩
        while left < right and window needs to shrink:
            # d 是将移出窗口的字符
            d = s[left]
            window.remove(d)
            # 缩小窗口
            left += 1
            # 进行窗口内数据的一系列更新
            ...
```
[3. Longest Substring Without Repeating Characters](https://labuladong.online/algo/essential-technique/sliding-window-framework/) <br>
[438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)<br>
[76. Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/description/)<br>
[567. Permutation in String](https://leetcode.com/problems/permutation-in-string/description/)<br>

有些题目就不需要windows 比如
[713. Subarray Product Less Than K](https://leetcode.com/problems/subarray-product-less-than-k/description/)

# 二分查找
细节实现是魔鬼 while的判断 left right指针的修改
[704. Binary Search](https://leetcode.com/problems/binary-search/description/)
[34. Find First and Last Position of Element in Sorted Array](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/description/)
```
#计算 mid 时需要防止溢出
#mid = left + (right - left) / 2 就和 (left + right) / 2 的结果相同，但是有效防止了 left 和 right 太大，直接相加导致溢出的情况。

```
## 左侧边界与右侧边界的二分查找

# 数组花式遍历技巧
1. 旋转一个nXn的二维数组
顺时针思路: 1. 按照正对角线交换数值，2. 再反转每一行的数字
逆时针思路: 1. 按照逆对角线交换数值  2. 再反转每一行的数字
<br>
[48. Rotate Image](https://leetcode.com/problems/rotate-image/)
<br>类似的还有 
[61. Rotate List](https://leetcode.com/problems/rotate-list/description/) **1. 反转整个链表 2.再当前k个和后面n-k个 再拼在一起**

2. 螺旋遍历nXm的数组
[54. Spiral Matrix](https://leetcode.com/problems/spiral-matrix/description/)
<br> **给予4个边界，遍历从左到右 上到下 右到左 下到上 四步 **循环的条件是目标res的数字个数和题目给的数字个数比较** 每次遍历一个部分后就移动边界, 比如左到右就让upperbound变化因为左到右把上边界遍历了一遍










