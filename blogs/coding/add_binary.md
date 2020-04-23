## Add Binary

Given two binary strings, return their sum (also a binary string).

The input strings are both *non-empty* and contains only characters `1` or `0`.

**Example:**

```
Input: a = "11", b = "1"
Output: "100"
```
```
Input: a = "1010", b = "1011"
Output: "10101"
```

**Constraints:**

* Each string consists only of `'0'` or `'1'` characters.
* `1 <= a.length, b.length <= 10^4`
* Each string is either `"0"` or doesn't contain any leading zero.

**Code:**

```python
class Solution:
    def addBinary(self, a, b) -> str:
        return '{0:b}'.format(int(a, 2) + int(b, 2))
```
Convert the string to an interger and then add, finally convert the result back to binary

```python
class Solution:
    def addBinary(self, a: str, b: str) -> str:
        ret = []
        i, j = len(a) - 1, len(b) - 1
        c = 0
        while i >= 0 or j >= 0:
            s = c
            if i >= 0:
                s += int(a[i])
                i -= 1
            if j >= 0:
                s += int(b[j])
                j -= 1
            c, s = divmod(s, 2)
            ret.append(str(s))
        if c:
            ret.append(str(c))
        return ''.join(ret[::-1])

```
Bit by bit addition with a carrier

```python
class Solution:
    def addBinary(self, a, b) -> str:
        x, y = int(a, 2), int(b, 2)
        while y:
            answer = x ^ y
            carry = (x & y) << 1
            x, y = answer, carry
        return bin(x)[2:]
```
Bit manipulation, x XOR y is the sum without carrier. x AND y shift 1 to the left is the carrier. We can keep adding them up until there's no carrier left.
