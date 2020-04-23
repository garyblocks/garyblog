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

```
class Solution(object):
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        stack = []
        mapping = {")": "(", "}": "{", "]": "["}

        # For every bracket in the expression.
        for char in s:
            # If the character is an closing bracket
            if char in mapping:
                top_element = stack.pop() if stack else '#'
                if mapping[char] != top_element:
                    return False
            else:
                # We have an opening bracket, simply push it onto the stack.
                stack.append(char)
        # The stack won't be empty for cases like ((()
        return not stack
```

