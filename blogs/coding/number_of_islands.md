## Number of Islands
Given a 2d grid map of `'1'`s (land) and `'0'`s (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

**Example:**

```
Input:
11110
11010
11000
00000

Output: 1
```
```
Input:
11000
11000
00100
00011

Output: 3
```

**Code:**

```python
class Solution:
    def numIslands(self, grid: List[List[str]]) -> int:
        def dfs(i, j):
            grid[i][j] = '0'
            for dx, dy in [(0, 1), (1, 0), (-1, 0), (0, -1)]:
                x, y = i + dx, j + dy
                if x < 0 or y < 0 or x >= len(grid) or y >= len(grid[0]):
                    continue
                if grid[x][y] == '1':
                    dfs(x, y)
        cnt = 0
        for i in range(len(grid)):
            for j in range(len(grid[0])):
                if grid[i][j] == '1':
                    cnt += 1
                    dfs(i, j)
        return cnt
```
loop through all the cells, if one cell is '1', count the element, then do a dfs search to make sure all the connected cells are turned to '0'.

