### 23. Merge k Sorted Lists

![Uploading image.png…]()

* 解題思路
假設是L1~L8 設計一個divide函數跟merge sort函數 \
divide一直切左右兩半 切到只剩下一個list \
因為這題有排序過的list 所以不用額外判斷 \
做merge sort L1跟L2merge、L3跟L4merge L12跟L34merge \
利用遞迴的設計 divide的每個小串列最後會merge回大串列 \
merge sort的函數 \
先初始化一個dummy變數 是listnode(0) \
變數l1、l2都指著最左邊的元素 \
兩個list元素按照順序比大小按照大小排序，更新current的下一個元素 \
return dummy.next

  
* 程式 
```python
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[Optional[ListNode]]
        :rtype: Optional[ListNode]
        """
        if not lists:
            return None
        return self.divide(lists, 0, len(lists)-1)

    def divide(self, lists, l, r):
        if l == r:
            return lists[l]

        mid = (l + r) // 2

        left = self.divide(lists, l, mid)
        right = self.divide(lists, mid+1, r)

        return self.merge(left, right)

    def merge(self, l1, l2):
        dummy = ListNode(0)
        cur = dummy

        while l1 and l2:
            if l1.val < l2.val:
                cur.next = l1
                l1 = l1.next
            else:
                cur.next = l2
                l2 = l2.next

            cur = cur.next

        if l1:
            cur.next = l1
        if l2:
            cur.next = l2

        return dummy.next        
