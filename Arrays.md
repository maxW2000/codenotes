# 双指针技巧

## 左右指针
[167. Two Sum II - Input Array Is Sorted](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/description/)

不需要考虑相对位置 如果考虑就需要用快慢指针 参考283. movezero
[27. Remove Element](https://leetcode.com/problems/remove-element/description/)

[344. Reverse String](https://leetcode.com/problems/reverse-string/description/)

[LCR 006. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/kLl5u1/description/)

## 快慢指针
一般都有一个快指针负责探路判断 慢指针负责处理结果 随后再增加
[26. Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/description/)

[283. Move Zeroes](https://leetcode.com/problems/move-zeroes/description/)

[83. Remove Duplicates from Sorted List](https://leetcode.com/problems/remove-duplicates-from-sorted-list/description/)

## 中心扩散指针
以每个元素为中心进行中心扩散去寻找回文串，并记录当前回文串的长度
[5. Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/description/)

## 滑动窗口
**本质也是指针 但是需要去维护这个窗口，这个窗口就是左右指针组成的 
思考什么时候缩小窗口 什么时候更新窗口，条件是什么**
- **windows**一般就是包含满足条件的字符
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
    while right < len(s):
        # c 是将移入窗口的字符
        c = s[right]
        window.add(c)
        # 增大窗口
        right += 1
        # 进行窗口内数据的一系列更新
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
[3. Longest Substring Without Repeating Characters](https://labuladong.online/algo/essential-technique/sliding-window-framework/)
[438. Find All Anagrams in a String](https://leetcode.com/problems/find-all-anagrams-in-a-string/description/)










