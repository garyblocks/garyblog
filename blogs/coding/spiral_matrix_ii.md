## Spiral Matrix II

Given a positive integer n, generate a square matrix filled with elements from 1 to \\(n^2\\) in spiral order.

**Example:**

```
Input: 3
Output:
[
 [ 1, 2, 3 ],
 [ 8, 9, 4 ],
 [ 7, 6, 5 ]
]
```

**Code:**

```
class Solution:
    def generateMatrix(self, n: int) -> List[List[int]]:
        matrix = [[0]*n for _ in range(n)]
        dires = [(0, 1), (1, 0), (0, -1), (-1, 0)]
        d = 0
        r, c = 0, 0
        for i in range(1, n**2+1):
            matrix[r][c] = i
            
            nr, nc = r + dires[d][0], c + dires[d][1]
            if nr < 0 or nc < 0 or nr >= n or nc >= n or matrix[nr][nc] != 0:
                d = (d + 1) % 4
            r, c = r + dires[d][0], c + dires[d][1]
        return matrix
```
