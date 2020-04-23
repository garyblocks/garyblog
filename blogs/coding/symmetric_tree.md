## Symmetric Tree
Given a binary tree, check whether it is a mirror of itself (ie, symmetric around its center).

For example, this binary tree `[1,2,2,3,4,4,3]` is symmetric:

```
    1
   / \
  2   2
 / \ / \
3  4 4  3
```

But the following `[1,2,2,null,3,null,3]` is not:

```
    1
   / \
  2   2
   \   \
   3    3
``` 

**Note:**
Bonus points if you could solve it both recursively and iteratively.

**Code:**

```python
class Solution(object):
    def isSymmetric(self, root):
        if not root:
            return True
        return self.compare(root.left, root.right)
    
    def compare(self, left, right):
        if not left and not right:
            return True
        if left and right:
            if left.val != right.val:
                return False
            return self.compare(left.left, right.right) and self.compare(left.right, right.left)
        return False
```
recursively, this is straight forward, just need to compare the value of paired nodes and also remember to do a mirror reflection when comparing the children.

```python
class Solution:
    def isSymmetric(self, root: TreeNode) -> bool:
        array = [root, root]
        while array:
            node1 = array.pop(0)
            node2 = array.pop(0)
            if not node1 and not node2:
                continue
            elif not node1 or not node2:
                return False
            elif node1.val != node2.val:
                return False
            array.extend([node1.left, node2.right, node1.right, node2.left])
        return True
```
iterately, we can use a list as an array, feed in the nodes to compare in right order and then poll two of them out each time from the head.
