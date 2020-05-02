# Partition Labels

A string S of lowercase letters is given. We want to partition this string into as many parts as possible so that each letter appears in at most one part, and return a list of integers representing the size of these parts.

**Example:**
```
Input: S = "ababcbacadefegdehijhklij"
Output: [9,7,8]
Explanation:
The partition is "ababcbaca", "defegde", "hijhklij".
This is a partition so that each letter appears in at most one part.
A partition like "ababcbacadefegde", "hijhklij" is incorrect, because it splits S into less parts.
```

**Note:**

* `S` will have length in range `[1, 500]`.
* `S` will consist of lowercase letters (`'a'` to `'z'`) only.

**Code:**

```python
class Solution:
    def partitionLabels(self, S: str) -> List[int]:
        if not S:
            return []
        last_pos = {}
        for i in range(len(S)-1, -1, -1):
            if S[i] not in last_pos:
                last_pos[S[i]] = i
        ret = []
        start, j = 0, 0
        for i in range(len(S)):
            j = max(j, last_pos[S[i]])
            if i == j:
                ret.append(j - start + 1)
                start = j + 1
        return ret
```
save all the last position of each character, then loop through the string, if all the words appears before a certain last appear position, it's the partition.
