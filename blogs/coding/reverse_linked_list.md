## Reverse Linked List
Reverse a singly linked list.

**Example:**

```
Input: 1->2->3->4->5->NULL
Output: 5->4->3->2->1->NULL
```
**Follow up:**

A linked list can be reversed either iteratively or recursively. Could you implement both?

**Code:**

```
def reverseList(self, head):
    if not head or not head.next:
    	return head
    p = self.reverseList(head.next)
    head.next.next = head
    head.next = null
    return p
```

