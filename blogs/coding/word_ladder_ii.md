## Word Ladder II
Given two words (*beginWord* and *endWord*), and a dictionary's word list, find all shortest transformation sequence(s) from *beginWord* to *endWord*, such that:

1. Only one letter can be changed at a time
2. Each transformed word must exist in the word list. Note that *beginWord* is not a transformed word.

**Note:**

* Return an empty list if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume beginWord and endWord are non-empty and are not the same.

**Example**:

```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]
Output:
[
  ["hit","hot","dot","dog","cog"],
  ["hit","hot","lot","log","cog"]
]
```
```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]
Output: []
Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```

**Code:**

```python
from collections import defaultdict
class Solution:
    def findLadders(self, beginWord: str, endWord: str, wordList: List[str]) -> List[List[str]]:
        front = {beginWord: [[beginWord]]}
        ret = []
        words = set(wordList)
        while front:
            new_front = defaultdict(list)
            for w in front:
                if w == endWord:
                    ret.extend(front[w])
                else:
                    for i in range(len(w)):
                        for c in 'abcdefghijklmnopqrstuvwxyz':
                            nw = w[:i] + c + w[i+1:]
                            if nw in words:
                                new_front[nw] += [p + [nw] for p in front[w]]
            words -= set(new_front.keys())
            if ret:
                break
            front = new_front
        return ret
```
Layer by layer BFS, use a dictionary to hold the last word.
