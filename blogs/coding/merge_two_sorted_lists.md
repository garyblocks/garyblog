## Merge Two Sorted Lists
Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

**Example:**

```
Input: 1->2->4, 1->3->4
Output: 1->1->2->3->4->4
```
**Code:**

```python
class Solution:
    def mergeTwoLists(self, l1, l2):
        if l1 is None:
            return l2
        elif l2 is None:
            return l1
        elif l1.val < l2.val:
            l1.next = self.mergeTwoLists(l1.next, l2)
            return l1
        else:
            l2.next = self.mergeTwoLists(l1, l2.next)
            return l2
```
This can be solved recursively, each time we pick the smaller node and merge the rest lists.

```python
class Solution:
    def mergeTwoLists(self, l1: ListNode, l2: ListNode) -> ListNode:
        ret = ListNode(0)
        curr = ret
        while l1 or l2:
            if not l1:
                curr.next = l2
                break
            elif not l2:
                curr.next = l1
                break
            elif l1.val > l2.val:
                curr.next = l2
                l2 = l2.next
                curr = curr.next
            else:
                curr.next = l1
                l1 = l1.next
                curr = curr.next
        return ret.next
```
To solve this iteratively, we can create a dummy node to hold the new list, than at each step, compare the values.
