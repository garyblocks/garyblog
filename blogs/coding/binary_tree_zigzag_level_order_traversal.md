## Binary Tree Zigzag Level Order Traversal
Given a binary tree, return the zigzag level order traversal of its nodes' values. (ie, from left to right, then right to left for the next level and alternate between).

For example:
Given binary tree `[3,9,20,null,null,15,7]`,

```
    3
   / \
  9  20
    /  \
   15   7
```
return its zigzag level order traversal as:

```
[
  [3],
  [20,9],
  [15,7]
]
```
**Code:**

```python
class Solution:
    def zigzagLevelOrder(self, root: TreeNode) -> List[List[int]]:
        layer = [root]
        ret = []
        level = 1
        while layer:
            new_layer = []
            values = []
            for node in layer:
                if not node:
                    continue
                values.append(node.val)
                if level % 2:
                    new_layer.extend([node.left, node.right])
                else:
                    new_layer.extend([node.right, node.left])
            if values:
                ret.append(values)
            layer = list(reversed(new_layer))
            level += 1
        return ret
```
BFS solution is going through it layer by layer, append from different direction for each layers. Always reverse the order at the end, be careful for the left and right leaves.

```python
from collections import deque

class Solution:
    def zigzagLevelOrder(self, root):
        """
        :type root: TreeNode
        :rtype: List[List[int]]
        """
        if root is None:
            return []

        results = []
        def dfs(node, level):
            if level >= len(results):
                results.append(deque([node.val]))
            else:
                if level % 2 == 0:
                    results[level].append(node.val)
                else:
                    results[level].appendleft(node.val)

            for next_node in [node.left, node.right]:
                if next_node is not None:
                    dfs(next_node, level+1)

        # normal level order traversal with DFS
        dfs(root, 0)

        return results
```
dfs is similar. 
