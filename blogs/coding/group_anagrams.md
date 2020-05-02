## Group Anagrams
Given an array of strings, group anagrams together.

**Note:**
	
* All inputs will be in lowercase.
* The order of your output does not matter.

**Example:**

```
Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
```
**Code:**

```python
from collections import defaultdict
class Solution:
    def groupAnagrams(self, strs: List[str]) -> List[List[str]]:
        groups = defaultdict(list)
        for wd in strs:
            swd = ''.join(sorted(wd))
            groups[swd].append(wd)
        return groups.values()
```
sort each word and use that as key to group the words into a hashtable. 

```python
class Solution:
    def groupAnagrams(strs):
        ans = collections.defaultdict(list)
        for s in strs:
            count = [0] * 26
            for c in s:
                count[ord(c) - ord('a')] += 1
            ans[tuple(count)].append(s)
        return ans.values()
```
group by character count, the key here is to count all 26 letters so we don't have to sort.

