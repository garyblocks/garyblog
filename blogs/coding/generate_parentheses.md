## Generate Parentheses

Given *n* pairs of parentheses, write a function to generate all combinations of well-formed parentheses.

**Example:**

```
given n = 3, a solution set is:

[
  "((()))",
  "(()())",
  "(())()",
  "()(())",
  "()()()"
]
```

**Code:**

```python
class Solution:
    def generateParenthesis(self, n: int) -> List[str]:
        self.ret = []
        self.dfs('', 0, n)
        return self.ret
    
    def dfs(self, path, left, right):
        if not left and not right:
            self.ret.append(path)
        if left:
            self.dfs(path + ')', left-1, right)
        if right:
            self.dfs(path + '(', left+1, right-1)
```
Using dfs, to keep track the result and also two variables, one for open parentheses and for parantheses to open