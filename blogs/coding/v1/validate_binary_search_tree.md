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
        def helper(node, lower=float('-inf'), upper=float('inf')):
            # empty node should be valid, it's easier for the recursion
            if not node:
                return True
            # check left and right, use or to cut down branches
            if not helper(node.left, lower, node.val) or not helper(node.right, node.val, upper):
                return False
            # check if the current node is valid
            return lower < node.val < upper
        return helper(root)
```
**Idea:** Divide and conquer recursively.

**Detail:**

* If the node is None, we return True to faciliate the recursion.
* Then check both left and right with dfs, the boundaries are updated for the recursive calls.
* Finally check if the current node's value resides in the boundaries.
* This is correct because the parent node's value is used as the boundary, and with be checked from the child nodes.

**Complexity:**

* Time complexity : *O(N)* since we visit each node exactly once.
* Space complexity : *O(N)* since we keep up to the entire tree.

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        stack, value = [], float('-inf')  # value to hold the current inorder value
        while stack or root:
            # put all the left nodes into stack
            while root:
                stack.append(root)
                root = root.left
            root = stack.pop()
            # if current value smaller than inorder value, not a BST
            if root.val <= value:
                return False
            # update value and check the right branch
            value = root.val
            root = root.right
        return True
```
**Idea:** Inorder tranverse all the nodes

**Detail:**

* Inorder tranverse goes like: left->root->right
* We need a stack to go through the left nodes, because inorder is the reverse of root->left
* To check the validity of each node, we can keep checking the current value with the largest value so far.
* At each step, we use a while loop to clear all the left nodes, then we check the root and move to the right.

**Complexity:**

* Time complexity : *O(N)* since we visit each node exactly once.
* Space complexity : *O(N)* since we keep up to the entire tree.

```python
class Solution:
    def isValidBST(self, root: TreeNode) -> bool:
        stack = [(root, float('-inf'), float('inf'))]
        while stack:
            node, min_, max_ = stack.pop()
            if not node:
                continue
            if node.val <= min_ or node.val >= max_:
                return False
            stack.append((node.left, min_, node.val))
            stack.append((node.right, node.val, max_))
        return True
```
**Idea:** Similar idea with the recursion

**Detail:**

* In the stack, keep all the states
* The check is the same as before

**Complexity:**

* Time complexity : *O(N)* since we visit each node exactly once.
* Space complexity : *O(N)* since we keep up to the entire tree.