## Reverse Nodes in k-Group
Given a linked list, reverse the nodes of a linked list *k* at a time and return its modified list.

*k* is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of k then left-out nodes in the end should remain as it is.

**Example:**

Given this linked list: `1->2->3->4->5`

For k = 2, you should return: `2->1->4->3->5`

For k = 3, you should return: `3->2->1->4->5`

**Note:**

* Only constant extra memory is allowed.
* You may not alter the values in the list's nodes, only nodes itself may be changed.

**Code:**

```python
class Solution:
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        dummy = ListNode(0, head)
        
        def rev(start, next_n):
            if start.next == next_n:
                return start
            tmp = start.next
            new_start = rev(tmp, next_n)
            tmp.next = start
            start.next = next_n
            return new_start
        
        cur, cnt = head, 0
        prev = dummy
        while cur:
            cur = cur.next
            cnt += 1
            if cnt % k == 0:
                new_prev = prev.next
                prev.next = rev(new_prev, cur)
                prev = new_prev
        return dummy.next
```
have two pointers, one as the node before k start, other one is after k ends, when we have k nodes, reverse these nodes.
