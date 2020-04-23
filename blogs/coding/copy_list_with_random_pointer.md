## Copy List with Random Pointer
A linked list is given such that each node contains an additional random pointer which could point to any node in the list or null.

Return a *deep copy* of the list.

The Linked List is represented in the input/output as a list of n nodes. Each node is represented as a pair of [val, random_index] where:

* `val`: an integer representing `Node.val`
* `random_index`: the index of the node (range from `0` to `n-1`) where random pointer points to, or `null` if it does not point to any node.

**Example:**

```
Input: head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
Output: [[7,null],[13,0],[11,4],[10,2],[1,0]]
```
```
Input: head = [[1,1],[2,1]]
Output: [[1,1],[2,1]]
```
```
Input: head = [[3,null],[3,0],[3,null]]
Output: [[3,null],[3,0],[3,null]]
```
```
Input: head = []
Output: []
Explanation: Given linked list is empty (null pointer), so return null.
```
**Constraints:**

* `-10000 <= Node.val <= 10000`
* `Node.random` is null or pointing to a node in the linked list.
* Number of Nodes will not exceed 1000.
**Code:**

```
class Solution(object):
    def __init__(self):
        # Dictionary which holds old nodes as keys and new nodes as its values.
        self.visitedHash = {}

    def copyRandomList(self, head):
        if head == None:
            return None
        if head in self.visitedHash:
            return self.visitedHash[head]
        # create a new node
        # with the value same as old node.
        node = Node(head.val, None, None)
        self.visitedHash[head] = node
        # Recursively copy the remaining linked list from the pointers.
        node.next = self.copyRandomList(head.next)
        node.random = self.copyRandomList(head.random)
        return node
```

