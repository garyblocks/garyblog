## Binary Tree Level Order Traversal
Given a binary tree, return the level order traversal of its nodes' values. (ie, from left to right, level by level).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```
return its level order traversal as:

```
[
  [3],
  [9,20],
  [15,7]
]
```
**Code:**

```python
from collections import deque
class Solution:
    def levelOrder(self, root: TreeNode) -> List[List[int]]:
        ret = []
        q = deque(['#', root])
        while q:
            node = q.popleft()
            if node == '#':
                if not q:
                    break
                ret.append([])
                q.append('#')
                continue
            elif node:
                ret[-1].append(node.val)
                q.append(node.left)
                q.append(node.right)
        if ret and not ret[-1]:
            return ret[:-1]
        return ret
```
Use a deque to BFS the tree, use '#' as delimiter of the layers. Remember to clean up the last layer in case of all 'None'
