## Lowest Common Ancestor of a Binary Tree

Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.

According to the definition of LCA on Wikipedia: “The lowest common ancestor is defined between two nodes p and q as the lowest node in T that has both p and q as descendants (where we *allow a node to be a descendant of itself*).”

Given the following binary tree:  root = `[3,5,1,6,2,0,8,null,null,7,4]`

**Example:**

```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
Output: 3
Explanation: The LCA of nodes 5 and 1 is 3.
```
```
Input: root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
Output: 5
Explanation: The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
```

**Note:**

* All of the nodes' values will be unique.
* p and q are different and both values will exist in the binary tree.

**Code:**

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        self.ret = None
        def help(node):
            if not node:
                return False
            left = help(node.left)
            right = help(node.right)
            mid = True if node is p or node is q else False
            if left + right + mid >= 2:
                self.ret = node
            return left or right or mid
        
        help(root)
        return self.ret
```
Recursively, we can check if each branch have p or q. The moment we have them on two branches, we got the LCA.

```python
class Solution:
    def lowestCommonAncestor(self, root: 'TreeNode', p: 'TreeNode', q: 'TreeNode') -> 'TreeNode':
        stack = [root]
        parents = {root: None}
        # find all parents for all nodes
        while p not in parents or q not in parents:
            node = stack.pop()
            if node.left:
                stack.append(node.left)
                parents[node.left] = node
            if node.right:
                stack.append(node.right)
                parents[node.right] = node
        # get all the parents for p
        pset = set()
        while p:
            pset.add(p)
            p = parents[p]
        # check q
        while q:
            if q in pset:
                return q
            q = parents[q]
```
Iterative solution, first, get all the parents before p and q, then find the path to p, if a point in q crosses the p path, it's the LCA.
