# Reorder List
Given a singly linked list *L: L0→L1→…→Ln-1→Ln*,
reorder it to: *L0→Ln→L1→Ln-1→L2→Ln-2→…*

You may not modify the values in the list's nodes, only nodes itself may be changed.

**Example:**

```
Given 1->2->3->4, reorder it to 1->4->2->3.
```
```
Given 1->2->3->4->5, reorder it to 1->5->2->4->3.
```

**Code:**

```python
class Solution:
    def reorderList(self, head: ListNode) -> None:
        """
        Do not return anything, modify head in-place instead.
        """
        if not head:
            return head
        # find middle point
        slow, fast = head, head
        while fast and fast.next:
            slow = slow.next
            fast = fast.next.next
        
        # reverse the node
        prev, cur = None, slow
        while cur:
            tmp = cur.next
            cur.next = prev
            prev = cur
            cur = tmp
        
        # merge
        while prev.next:
            tmp = head.next
            head.next = prev
            head = tmp
            tmp = prev.next
            prev.next = head
            prev = tmp
```
split the process into three steps, find the middle point, reverse the second list and finally merge two lists. When merging, since there's still one link left from the end of first list to the end of second, so we have to check the .next of the second list to know if it reaches the end.