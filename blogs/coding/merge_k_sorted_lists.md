## Merge k Sorted Lists
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

**Example:**

```
Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```
**Code:**

```python
class Solution:
    def mergeKLists(self, lists: List[ListNode]) -> ListNode:
        if not lists:
            return None
        l1 = lists[0]
        for l2 in lists[1:]:
            dummy = ListNode(0)
            cur = dummy
            while l1 or l2:
                if not l1:
                    cur.next = l2
                    break
                if not l2:
                    cur.next = l1
                    break
                if l1.val < l2.val:
                    cur.next = l1
                    l1 = l1.next
                    cur = cur.next
                else:
                    cur.next = l2
                    l2 = l2.next
                    cur = cur.next
            l1 = dummy.next
        return l1
```
Repeatedly merge two lists together, the time complexity is O(Nk)

```python
from Queue import PriorityQueue

class Solution(object):
    def mergeKLists(self, lists):
        head = point = ListNode(0)
        q = PriorityQueue()
        for l in lists:
            if l:
                q.put((l.val, l))
        while not q.empty():
            val, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            if node:
                q.put((node.val, node))
        return head.next
```
Use PriorityQueue to keep a heap of smallest nodes.
