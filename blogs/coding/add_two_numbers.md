## Add Two Numbers
You are given two *non-empty* linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

**Example:**

```
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```
**Code:**

```python
class Solution:
    def addTwoNumbers(self, l1: ListNode, l2: ListNode) -> ListNode:
        carrier = 0
        ret = ListNode(0)
        node = ret
        while l1 or l2:
            n1 = l1.val if l1 else 0
            n2 = l2.val if l2 else 0
            carrier, s = divmod(n1 + n2 + carrier, 10)
            node.next = ListNode(s)
            node = node.next
            l1 = l1.next if l1 else l1
            l2 = l2.next if l2 else l2
        if carrier:
            node.next = ListNode(carrier)
        return ret.next
```
We are doing the digit by digit addition for l1 and l2. To do so, we loop through both link lists, and keep a carrier to save any carrier count. If one list is empty, we use 0 instead. Beside, a dummy node is added to keep the list head for return.
