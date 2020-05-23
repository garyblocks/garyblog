# Word Break

Given a *non-empty* string s and a dictionary wordDict containing a list of *non-empty* words, determine if s can be segmented into a space-separated sequence of one or more dictionary words.

**Note:**

* The same word in the dictionary may be reused multiple times in the segmentation.
* You may assume the dictionary does not contain duplicate words.

**Example:**

```
Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
```
```
Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
```
```
Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```

**Code:**

```python
class Solution:
    seen = {'': True}
    def wordBreak(self, s: str, wordDict: List[str]) -> bool:
        if s in self.seen:
            return self.seen[s]
        for w in wordDict:
            if s.startswith(w):
                if self.wordBreak(s[len(w):], wordDict):
                    self.seen[s] = True
                    return True
        self.seen[s] = False
        return False
```
dfs with memorization.