# Remove Nth Node From End of List

Given a linked list, remove the n-th node from the end of list and return its head.

**Example:**

```
Given linked list: 1->2->3->4->5, and n = 2.

After removing the second node from the end, the linked list becomes 1->2->3->5.
```

**Note:**
Given n will always be valid.

**Follow up:**
Could you do this in one pass?

**Code:**

```python
class Solution:
    def removeNthFromEnd(self, head: ListNode, n: int) -> ListNode:
        dummy = ListNode(0)
        dummy.next = head
        l = 0
        while head:
            head = head.next
            l += 1
        cnt = 1
        curr = dummy
        while cnt < l - n + 1:
            curr = curr.next
            cnt += 1
        curr.next = curr.next.next
        return dummy.next
```
2 pass, get the length first then, find the node.
