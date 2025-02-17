# 链表
**dummyhead，dummytail 的妙用：每次指定一个dummyhead或dummytail可以有效的规避边界问题 (单双链表)**

## 双指针解决链表问题
### 快慢指针
[141. Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/description/) 
<br> 快慢指针解决 一快一慢，一步两步，相遇就说明有环, **先走再判断** 如果不走就判断，当只有一个节点的时候就会出问题

[142. Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/description/)
快指针一定走了2k步 慢指针走了k步相遇 所以快指针比慢指针多走了k步 就是环的大小，设他们在m位置相遇 则其余环的大小为k - m 则为从相遇点到环起点的位置，这个距离也是从head到环起点的位置，这是因为慢指针走了k步 且在环的m位置相遇<br>
所以只需要让他们相遇 然后把其中一个指向起点 再共同走一步 直到相遇 这个点就是环的起点

#### **分解链表技巧**
创造两个dummyhead 通过条件判断 分别把链表拆成两个部分，记得要断开原来的链表
[82. Remove Duplicates from Sorted List II](https://leetcode.com/problems/remove-duplicates-from-sorted-list-ii/description/)
```
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def deleteDuplicates(self, head: Optional[ListNode]) -> Optional[ListNode]:
        
        #因为val<=100 所以有可能会有负数 如果dummy设置为负数也成重复节点了
        #连接不相同的节点
        dummy1 = ListNode(101)
        #连接相同的节点
        dummy2 = ListNode(101)

        if not head: 
            return None

        #双指针
        pUniq,pDup = dummy1, dummy2
        p = head
        while p:
            #发现重复节点
            if (p.next is not None and p.val == p.next.val) or p.val == pDup.val:
                pDup.next = p

                pDup = pDup.next
            else:
                pUniq.next = p
                pUniq = pUniq.next

            p = p.next
            # 将原链表和新链表断开
            pUniq.next = None
            pDup.next = None
        
        return dummy1.next
            
```

## 反转链表
[206. Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/description/)

**由于单链表的结构，至少要用三个指针才能完成迭代反转** <br>
pre, cur, nex 三个指针 一个一个反转
```
#反转当前节点
cur.next = pre

#指针更新 向后移动过
pre = cur
cur = nex
if nex is not None:
    nex = nex.next
```

[92. Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list/description/)
反转链表的一部分
**去看反转前N个是怎么反转的 最后head就是反转后的尾节点 指向cur就可以**
**当成一个以left为起点 反转前right - left + 1的链表**
```
def reverseBetween(self, head: Optional[ListNode], left: int, right: int) -> Optional[ListNode]:
        
        # 把他当成反转前n个链表 只是以left为起点 前n个节点为right - left + 1
        # 就是反转一个以 left为起点的链表（后面的都算上）
        if left == 1:
            return self.reverseN(head, left)
        
        pre = head
        # 找left的前一个结点
        for i in range(1, left - 1):
            pre = pre.next
        # 从第 left 个节点开始反转
        pre.next = self.reverseN(pre.next, right - left + 1)

        return head
    
    def reverseN(self, head: Optional[ListNode], n: int) -> Optional[ListNode]:
        while head is None or head.next is None:
            return head
        
        pre, cur, nex = None, head, head.next
        while n > 0:
            cur.next = pre
            pre = cur
            cur = nex
            if nex is not None:
                nex = nex.next
            n -= 1
        
        # 以当前pre为全新的head
        # 此时的 cur 是第 n + 1 个节点，head 是反转后的尾结点
        head.next = cur

b       # 此时的 pre 是反转后的头结点
        return pre
```

[25. Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/description/)
递归实现 [具体思路](https://labuladong.online/algo/data-structure/reverse-linked-list-recursion/#%E6%9C%80%E5%90%8E%E6%80%BB%E7%BB%93)
把问题分解成 以k个为一个的子链表
1. a指针反转前k个链表 (reserveN(head, n))函数
2. b指针指向下一个子链表 
3. 返回第一步 递归到调用主函数到尾


