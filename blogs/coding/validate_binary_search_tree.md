## Validate Binary Search Tree
Given a binary tree, determine if it is a valid binary search tree (BST).

Assume a BST is defined as follows:

* The left subtree of a node contains only nodes with keys *less than* the node's key.
* The right subtree of a node contains only nodes with keys *greater than* the node's key.
* Both the left and right subtrees must also be binary search trees.
 

**Example:**

```
    2
   / \
  1   3

Input: [2,1,3]
Output: true
```
```
    5
   / \
  1   4
     / \
    3   6

Input: [5,1,4,null,null,3,6]
Output: false
Explanation: The root node's value is 5 but its right child's value is 4.
```

**Code:**

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        return self.validate(root)
    
    def validate(self, root, low=float('-inf'), high=float('inf')):
        if not root:
            return True
        
        if root.val <= low or root.val >= high:
            return False
        
        if not self.validate(root.left, low, root.val):
            return False
        if not self.validate(root.right, root.val, high):
            return False
        
        return True
```
It's a recursion solution, we keep track of the lower bound and upper bound of the subtree, if the node value is smaller than the lower bound or higher than the upper bound, we know it's invalid. And we recursively do that for both left and right tree. Both the time and space complexity of this solution is O(N).

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        if not root:
            return True
        
        stack = [(root, float('-inf'), float('inf'))]
        while stack:
            root, lower, upper = stack.pop()
            if not root:
                continue
            if root.val <= lower or root.val >= upper:
                return False
            stack.append((root.left, lower, root.val))
            stack.append((root.right, root.val, upper))
        return True
```
Here is an iteration solution, the idea is the same, but we are using a stack to keep track of the nodes to check.