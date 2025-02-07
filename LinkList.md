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
