## Diameter of Binary Tree

Given a binary tree, you need to compute the length of the diameter of the tree. The diameter of a binary tree is the length of the *longest* path between any two nodes in a tree. This path may or may not pass through the root.

**Example:**

Given a binary tree

```
          1
         / \
        2   3
       / \     
      4   5    
```
Return *3*, which is the length of the path `[4,2,1,3]` or `[5,2,1,3]`.

**Note:** The length of path between two nodes is represented by the number of edges between them.

**Code:**

```python
class Solution:
    def diameterOfBinaryTree(self, root: TreeNode) -> int:
        def helper(node):
            if not node:
                return 0, 0
            l_max, l_height = helper(node.left)
            r_max, r_height = helper(node.right)
            max_d = max(l_max, r_max, l_height + 1 + r_height)
            height = max(l_height, r_height) + 1
            return max_d, height
        
        md, h = helper(root)
        return max(0, md-1)
```
divide and conquer, use two variales to keep the states, height and max length.
