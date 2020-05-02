# Word Search II

Given a 2D board and a list of words from the dictionary, find all words in the board.

Each word must be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once in a word.

**Example:**

```
Input: 
board = [
  ['o','a','a','n'],
  ['e','t','a','e'],
  ['i','h','k','r'],
  ['i','f','l','v']
]
words = ["oath","pea","eat","rain"]

Output: ["eat","oath"]
```
 
**Note:**

* All inputs are consist of lowercase letters a-z.
*  The values of words are distinct.

**Code:**

```python
class Solution:
    def findWords(self, board: List[List[str]], words: List[str]) -> List[str]:
        if not board or not words:
            return []
        
        prefix_map = {}
        for wd in words:
            for i in range(1, len(wd)+1):
                prefix_map[wd[:i]] = 0
        words = set(words)
        ret = set()
        M, N = len(board), len(board[0])
        #print(prefix_map)
        
        def backtrack(i, j, path, seen):
            if path in words:
                ret.add(path)
            for dx, dy in [(0, 1), (1, 0), (-1, 0), (0, -1)]:
                x, y = i + dx, j + dy
                if 0 <= x < M and 0 <= y < N and (x, y) not in seen:
                    new = board[x][y]
                    if path + new in prefix_map:
                        seen.add((x, y))
                        backtrack(x, y, path+new, seen)
                        seen.remove((x, y))
            
        for i in range(M):
            for j in range(N):
                if board[i][j] in prefix_map:
                    backtrack(i, j, board[i][j], {(i, j)})
        return list(ret)
```
create a prefix hashmap to save all the prefixs, then use backtrack dfs to search each start position. Prune if the path not in the prefix map.
