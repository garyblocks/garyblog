## Roman to Integer

Roman numerals are represented by seven different symbols: `I`, `V`, `X`, `L`, `C`, `D` and `M`.

```
Symbol       Value
I             1
V             5
X             10
L             50
C             100
D             500
M             1000
```
For example, two is written as `II` in Roman numeral, just two one's added together. Twelve is written as, `XII`, which is simply `X` + `II`. The number twenty seven is written as `XXVII`, which is `XX` + `V` + `II`.

Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not `IIII`. Instead, the number four is written as `IV`. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as `IX`. There are six instances where subtraction is used:

* `I` can be placed before `V` (5) and `X` (10) to make 4 and 9. 
`X` can be placed before `L` (50) and `C` (100) to make 40 and 90. 
`C` can be placed before `D` (500) and `M` (1000) to make 400 and 900.
Given a roman numeral, convert it to an integer. Input is guaranteed to be within the range from 1 to 3999.

**Example:**

```
Input: "III"
Output: 3
```
```
Input: "IV"
Output: 4
```
```
Input: "IX"
Output: 9
```
```
Input: "LVIII"
Output: 58
Explanation: L = 50, V= 5, III = 3.
```
```
Input: "MCMXCIV"
Output: 1994
Explanation: M = 1000, CM = 900, XC = 90 and IV = 4.
```

**Code:**

```python
from collections import OrderedDict
class Solution:
    def romanToInt(self, s: str) -> int:
        m = OrderedDict([
            ('M', 1000), ('CM', 900), ('D', 500), ('CD', 400), ('C', 100),
            ('XC', 90), ('L', 50), ('XL', 40), ('X', 10), ('IX', 9),
            ('V', 5), ('IV', 4), ('III', 3), ('II', 2), ('I', 1)
        ])
        ret = 0
        for key in m:
            while s.startswith(key):
                s = s[len(key):]
                ret += m[key]
        return ret
```
#### Idea
Loop the values from bigger to smaller.

#### Detail
Use OrderedDict to loop the values from bigger to smaller, which is from left to right in the string. when a character appear twice or three times, use a while loop to check those them more than one times.