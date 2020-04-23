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

```
class Solution:
    def reverseLinkedList(self, head, k):
        new_head, ptr = None, head
        while k:
            next_node = ptr.next
            # Insert the node pointed to by "ptr"
            # at the beginning of the reversed list
            ptr.next = new_head
            new_head = ptr 
            # Move on to the next node
            ptr = next_node
            # Decrement the count of nodes to be reversed by 1
            k -= 1
        # Return the head of the reversed list
        return new_head
                
    
    def reverseKGroup(self, head: ListNode, k: int) -> ListNode:
        count = 0
        ptr = head
        while count < k and ptr:
            ptr = ptr.next
            count += 1    
        # If we have k nodes, then we reverse them
        if count == k: 
            reversedHead = self.reverseLinkedList(head, k)
            # we use that and the "original" head of the "k" nodes
            # to re-wire the connections.
            head.next = self.reverseKGroup(ptr, k)
            return reversedHead
        return head
```

