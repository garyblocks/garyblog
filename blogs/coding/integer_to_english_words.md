## Integer to English Words
Convert a non-negative integer to its english words representation. Given input is guaranteed to be less than \\( 2^{31} - 1 \\).

**Example:**

```
Input: 123
Output: "One Hundred Twenty Three"
```
```
Input: 12345
Output: "Twelve Thousand Three Hundred Forty Five"
```
```
Input: 1234567
Output: "One Million Two Hundred Thirty Four Thousand Five Hundred Sixty Seven"
```
```
Input: 1234567891
Output: "One Billion Two Hundred Thirty Four Million Five Hundred Sixty Seven Thousand Eight Hundred Ninety One"
```
**Code:**

```python
class Solution:
    def numberToWords(self, num: int) -> str:
        if not num:
            return 'Zero'
        ret = []
        digits = [
            'Zero', 'One', 'Two', 'Three', 'Four', 'Five', 'Six', 'Seven', 'Eight', 'Nine', 
            'Ten', 'Eleven', 'Twelve', 'Thirteen', 'Fourteen', 'Fifteen', 'Sixteen',
            'Seventeen', 'Eighteen', 'Nineteen'
        ]
        tens = ['Zero', 'Ten', 'Twenty', 'Thirty', 'Forty', 'Fifty', 'Sixty', 'Seventy', 'Eighty', 'Ninety']
        def parse(n):
            r = []
            if n >= 100:
                count, n = divmod(n, 100)
                r += [digits[count], 'Hundred']
            if n >= 20:
                count, n = divmod(n, 10)
                r.append(tens[count])
            if n:
                r.append(digits[n])
            return r
            
        # divide
        parts = []
        while num:
            num, part = divmod(num, 1000)
            parts.append(part)
        if len(parts) == 4:
            ret += [digits[parts[3]], "Billion"]
        if len(parts) >= 3:
            nums = parse(parts[2])
            if nums:
                ret += nums
                ret.append('Million')
        if len(parts) >= 2:
            nums = parse(parts[1])
            if nums:
                ret += nums
                ret.append('Thousand')
        nums = parse(parts[0])
        ret += nums
        return ' '.join(ret)
```
Divide by digit count and conquer. Be careful with 0.

