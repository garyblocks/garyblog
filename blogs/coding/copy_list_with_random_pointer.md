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

```python
class Solution:
    def copyRandomList(self, head: 'Node') -> 'Node':
        if not head:
            return head
        node_map = {}
        tmp = head
        while head:
            node_map[head] = Node(head.val)
            head = head.next
        new_head = node_map[tmp]
        
        while tmp:
            if tmp.next:
                node_map[tmp].next = node_map[tmp.next]
            if tmp.random:
                node_map[tmp].random = node_map[tmp.random]
            tmp = tmp.next
        return new_head
```
Run through the linked list twice, the first time create all new nodes and keep the mapping in a dictionary, the second time link the next and random.
