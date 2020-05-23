## Binary Tree Maximum Path Sum
Given a *non-empty* binary tree, find the maximum path sum.

For this problem, a path is defined as any sequence of nodes from some starting node to any node in the tree along the parent-child connections. The path must contain at least one node and does not need to go through the root.

**Example:**

```
Input: [1,2,3]

       1
      / \
     2   3

Output: 6
```
```
Input: [-10,9,20,null,null,15,7]

   -10
   / \
  9  20
    /  \
   15   7

Output: 42
```
**Code:**

```python
class Solution:
    def maxPathSum(self, root: TreeNode) -> int:
        self.max_sum = float('-inf')
        def get_sum(node):
            max_left = get_sum(node.left) + node.val if node.left else node.val
            max_right = get_sum(node.right) + node.val if node.right else node.val
            self.max_sum = max(
                self.max_sum, node.val,
                max_left, max_right,
                max_left + max_right - node.val
            )
            return max(max_left, node.val, max_right)
        
        get_sum(root)
        return self.max_sum
```
Keep checking left, right, start from mid or left + mid + right.

