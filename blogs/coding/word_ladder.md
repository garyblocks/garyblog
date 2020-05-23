## Word Ladder
Given two words (*beginWord* and *endWord*), and a dictionary's word list, find the length of shortest transformation sequence from *beginWord* to *endWord*, such that:

1. Only one letter can be changed at a time.
2. Each transformed word must exist in the word list. Note that *beginWord* is not a transformed word.

**Note:**

* Return 0 if there is no such transformation sequence.
* All words have the same length.
* All words contain only lowercase alphabetic characters.
* You may assume no duplicates in the word list.
* You may assume *beginWord* and *endWord* are non-empty and are not the same.

**Example:**

```
Input:
beginWord = "hit",
endWord = "cog",
wordList = ["hot","dot","dog","lot","log","cog"]

Output: 5

Explanation: As one shortest transformation is "hit" -> "hot" -> "dot" -> "dog" -> "cog",
return its length 5.
```
```
Input:
beginWord = "hit"
endWord = "cog"
wordList = ["hot","dot","dog","lot","log"]

Output: 0

Explanation: The endWord "cog" is not in wordList, therefore no possible transformation.
```
**Code:**

```python
class Solution:
    def ladderLength(self, beginWord: str, endWord: str, wordList: List[str]) -> int:
        words = set(wordList)
        step = 1
        front = {beginWord}
        while front and endWord not in front:
            step += 1
            new_front = set()
            for w in front:
                for i in range(len(w)):
                    for x in 'abcdefghijklmnopqrstuvwxyz':
                        new = w[:i] + x + w[i+1:]
                        if new in words:
                            if new == endWord:
                                return step
                            words.remove(new) 
                            new_front.add(new)
            front = new_front
        return 0
```
BFS, loop through the possible new words and also remove the seen words as they are not going to generate shorter paths.

