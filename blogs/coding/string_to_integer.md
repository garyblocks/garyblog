## String to Integer (atoi)
Implement `atoi` which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

**Note:**

* Only the space character `' '` is considered as whitespace character.
* Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−2^31,  2^31 − 1]. If the numerical value is out of the range of representable values, INT_MAX (2^31 − 1) or INT_MIN (−2^31) is returned.

**Example:**

```
Input: "42"
Output: 42
```
```
Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
```
```
Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
```
```
Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
```
```
Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.
```
**Code:**

```python
class Solution:
    def myAtoi(self, str: str) -> int:
        threshold = 2**31 // 10
        # remove white space
        str = str.strip()  # need to keep the space in the middle
        if len(str) == 0: return 0
        
        # check sign
        i = 0
        sign = 1
        if str[i] in '+-':
            if str[i] == '-':
                sign = -1
            i += 1
            
        # get the numerical part
        ret = 0
        while i < len(str):
            if not str[i].isdigit():
            	   # handle trailing characters
                break
            n = ord(str[i]) - ord('0')
            # need to handle the overflow one step in advance
            if sign < 0 and (ret > threshold or ret == threshold and n > 8):
                return -2**31
            elif sign > 0 and (ret > threshold or ret == threshold and n > 7):
                return 2**31 - 1
            ret = ret * 10 + n
            i += 1
        
        return sign * ret
```
Just go through the string character by character, but a lot of corner cases need to mind. When you split the logic into units, it's easier to manage.

A trick here is that check length is faster than if not.