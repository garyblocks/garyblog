# Serialize and Deserialize Binary Tree

Serialization is the process of converting a data structure or object into a sequence of bits so that it can be stored in a file or memory buffer, or transmitted across a network connection link to be reconstructed later in the same or another computer environment.

Design an algorithm to serialize and deserialize a binary tree. There is no restriction on how your serialization/deserialization algorithm should work. You just need to ensure that a binary tree can be serialized to a string and this string can be deserialized to the original tree structure.

**Example:**

```
You may serialize the following tree:

    1
   / \
  2   3
     / \
    4   5

as "[1,2,3,null,null,4,5]"
```

**Clarification:** The above format is the same as how LeetCode serializes a binary tree. You do not necessarily need to follow this format, so please be creative and come up with different approaches yourself.

**Note:** Do not use class member/global/static variables to store states. Your serialize and deserialize algorithms should be stateless.

**Code:**

```python
from collections import deque

class Codec:

    def serialize(self, root):
        """Encodes a tree to a single string.
        
        :type root: TreeNode
        :rtype: str
        """
        ret = []
        queue = deque([root])
        while queue:
            node = queue.pop()
            if not node:
                ret.append('#')
            else:
                queue.appendleft(node.left)
                queue.appendleft(node.right)
                ret.append(str(node.val))
        return ','.join(ret)
        
    def deserialize(self, data):
        """Decodes your encoded data to tree.
        
        :type data: str
        :rtype: TreeNode
        """
        nodes = data.split(',')
        if nodes[0] == '#':
            head = None
        else:
            head = TreeNode(int(nodes[0]))
        queue = deque([head])
        for i in range(1, len(nodes), 2):
            curr = queue.pop()
            if nodes[i] == '#':
                curr.left = None
            else:
                leftnode = TreeNode(int(nodes[i]))
                curr.left = leftnode
                queue.appendleft(leftnode)
            if nodes[i+1] == '#':
                curr.right = None
            else:
                rightnode = TreeNode(int(nodes[i+1]))
                curr.right = rightnode
                queue.appendleft(rightnode)
        return head
```
Took a BFS approach, use the queue to iterate on nodes, in the deserialize part, we are processing two nodes at a time.
