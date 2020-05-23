## Letter Combinations of a Phone Number

Given a string containing digits from `2-9` inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

**Example:**

```
Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].
```

**Note:**
Although the above answer is in lexicographical order, your answer could be in any order you want.

**Code:**

```python
class Solution:
    def letterCombinations(self, digits: str) -> List[str]:
        map_ = {
            "2": 'abc',
            "3": 'def',
            "4": 'ghi',
            "5": 'jkl',
            "6": 'mno',
            "7": 'pqrs',
            "8": 'tuv',
            "9": 'wxyz'
        }
        ret = []
        def dfs(path, digits):
            if not digits:
            		# end condition is not more digits
                return ret.append(path)
            for d in map_[digits[0]]:
                dfs(path + d, digits[1:])
        if digits:  # make sure empty list is returned
            dfs("", digits)
        return ret
```
We are doing a DFS search to generate all the possible combinations one by one. The corner case here is to check if there's no digit to begin with, we should return empty list. DFS is better here because it saves a lot of initialization or checking working in BFS.

Time and space complexity are both \\(3^N \times 4^M\\), N is the number of digits that map to three letters and M is number of digits that map to four letters.
