## Implement strStr()
Implement *strStr()*.

Return the index of the first occurrence of needle in haystack, or -1 if needle is not part of haystack.

**Example:**

```
Input: haystack = "hello", needle = "ll"
Output: 2
```
```
Input: haystack = "aaaaa", needle = "bba"
Output: -1
```
**Clarification:**

What should we return when `needle` is an empty string? This is a great question to ask during an interview.

For the purpose of this problem, we will return 0 when `needle` is an empty string. This is consistent to C's *strstr()* and Java's *indexOf()*.

**Code:**

```python
def strStr(self, haystack, needle):
    for i in range(len(haystack) - len(needle)+1):
        if haystack[i:i+len(needle)] == needle:
            return i
    return -1
```
Plain string comparison

```python
class Solution:
    def strStr(self, haystack: str, needle: str) -> int:
        if not needle:
            return 0
        mod =2**31
        hn = 0
        for c in needle:
            hn = (hn * 26 + ord(c) - ord('a') + 1) % mod
        l = len(needle)
        
        hr = 0
        for i, c in enumerate(haystack):
            if i >= l:
                left = ord(haystack[i - l]) - ord('a') + 1
                hr -= left * 26 ** (l - 1)
            hr = (hr * 26 + ord(c) - ord('a') + 1) % mod
            if hr == hn:
                return i - l + 1
        return -1
```
Use rolling hash
