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
        carry = 0
        dummy_node = ListNode(0)  # easier to return the result
        curr = dummy_node
        while l1 or l2:
            sum_ = carry
            if l1:
                sum_ += l1.val
                l1 = l1.next
            if l2:
                sum_ += l2.val
                l2 = l2.next
            carry, r = divmod(sum_, 10)
            curr.next = ListNode(r)
            curr = curr.next
        if carry:
            # if there's a carry left, add that too
            curr.next = ListNode(carry)
        return dummy_node.next
```

**Idea:** Node by node summation with a carry variable.

**Detail:**

* Calculate the sum along the loop with a carry variable.
* Build the result node by node in a new linked list.

**Complexity:**

* **Time complexity:**  \\(O(max(m,n))\\). Assume that \\(m\\) and \\(n\\) represents the length of `l1` and `l2` respectively, the algorithm above iterates at most \\(max(m, n)\\) times.

* **Space complexity:** \\(O(max(m,n))\\). The length of the new list is at most \\(\max(m,n) + 1\\).

