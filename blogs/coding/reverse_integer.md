## Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer.

**Example:**

```
Input: 123
Output: 321
```
```
Input: -123
Output: -321
```
```
Input: 120
Output: 21
```

**Note:**

Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: \\([−2^{31},  2^{31} − 1]\\). For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

**Code:**

```python
class Solution:
    def reverse(self, x: int) -> int:
        sign = 1 if x >= 0 else -1
        int_str = str(x)
        int_str = int_str[::-1].strip('-')
        rev_int = sign * int(int_str)
        if -2**31 < rev_int < 2**31 - 1:
            return rev_int
        else:
            return 0
```
The idea is just to convert int to string and reverse it then convert back. Two things to be careful are the negative sign and boundry.

```python
class Solution:
    def reverse(self, x: int) -> int:
        ret = 0  # if x is zero, it will pass the loop
        max_int = 2**31 // 10  # we need to check maximum before one step before
        # take out sign to let divmod run correctly
        sign = 1 if x >= 0 else -1
        x = abs(x)
        while x:
            # pop digit from x
            x, r = divmod(x, 10)
            # check for overflow
            if ret > max_int:
                return 0
            elif ret == max_int:
                # last digit of max int is 7 and min int is 8
                if (sign > 0 and r > 7) or (sign < 0 and r > 8):
                    return 0
            # push digit to ret
            ret = ret * 10 + r
        return sign * ret  # remember to put the sign back
```
Loop through the numbers using mode. Several things to be careful:
1. In python mod behave differently when the number is negative.
2. A lot of operations here, be sure to add parentheses.
3. The overflow check needs to be done one digit before hand to avoid overflow.
