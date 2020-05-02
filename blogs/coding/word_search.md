# Word Search
Given a 2D board and a word, find if the word exists in the grid.

The word can be constructed from letters of sequentially adjacent cell, where "adjacent" cells are those horizontally or vertically neighboring. The same letter cell may not be used more than once.

**Example:**

```
board =
[
  ['A','B','C','E'],
  ['S','F','C','S'],
  ['A','D','E','E']
]

Given word = "ABCCED", return true.
Given word = "SEE", return true.
Given word = "ABCB", return false.
```

**Constraints:**

* `board` and `word` consists only of lowercase and uppercase English letters.
* `1 <= board.length <= 200`
* `1 <= board[i].length <= 200`
* `1 <= word.length <= 10^3`

**Code:**

```python
class Solution:
    def exist(self, board: List[List[str]], word: str) -> bool:
        M, N = len(board), len(board[0])
        L = len(word) - 1
        def dfs(i, j, l, seen):
            if board[i][j] != word[l]:
                return False
            if l == L:
                return True
            for dx, dy in [[0, 1], [1, 0], [-1, 0], [0, -1]]:
                x, y = i + dx, j + dy
                if M > x >= 0 and N > y >=0 and (x, y) not in seen:
                    seen.add((x, y))
                    if dfs(x, y, l+1, seen):
                        return True
                    seen.remove((x, y))
            return False
            
        for i in range(M):
            for j in range(N):
                if dfs(i, j, 0, {(i, j)}):
                    return True
        return False
```

Start from each letter, check if it can form the word, keep a seen set to avoid duplicated letters.
