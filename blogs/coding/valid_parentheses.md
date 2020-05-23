## Valid Parentheses
Given a string containing just the characters `'('`, `')'`, `'{'`, `'}'`, `'['` and `']'`, determine if the input string is valid.

An input string is valid if:

1. Open brackets must be closed by the same type of brackets.
2. Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

**Example:**

```
Input: "()"
Output: true
```
```
Input: "()[]{}"
Output: true
```
```
Input: "(]"
Output: false
```
```
Input: "([)]"
Output: false
```
```
Input: "{[]}"
Output: true
```
**Code:**

```python
class Solution:
    def isValid(self, s: str) -> bool:
        stack = []
        pmap = {'(': ')', '[': ']', '{': '}'}
        for p in s:
            if p in pmap:
                stack.append(p)
            elif stack:
                sp = stack.pop()
                if p != pmap[sp]:
                    return False
            else:
                return False
        if stack:
            return False
        return True
```
#### Idea
Use a stack to keep track the last open parenthese.
