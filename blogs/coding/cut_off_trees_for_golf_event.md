## Cut Off Trees for Golf Event

You are asked to cut off trees in a forest for a golf event. The forest is represented as a non-negative 2D map, in this map:

* `0` represents the `obstacle` can't be reached.
* `1` represents the `ground` can be walked through.
* `The place with number bigger than 1` represents a `tree` can be walked through, and this positive number represents the tree's height.

In one step you can walk in any of the four directions `top`, `bottom`, `left` and `right` also when standing in a point which is a tree you can decide whether or not to cut off the tree.

You are asked to cut off *all* the trees in this forest in the order of tree's height - always cut off the tree with lowest height first. And after cutting, the original place has the tree will become a grass (value 1).

You will start from the point (0, 0) and you should output the minimum steps *you need to walk* to cut off all the trees. If you can't cut off all the trees, output -1 in that situation.

You are guaranteed that no two trees have the same height and there is at least one tree needs to be cut off.

**Example:**

```
Input: 
[
 [1,2,3],
 [0,0,4],
 [7,6,5]
]
Output: 6
```
```
Input: 
[
 [1,2,3],
 [0,0,0],
 [7,6,5]
]
Output: -1
```
```
Input: 
[
 [2,3,4],
 [0,0,5],
 [8,7,6]
]
Output: 6
Explanation: You started from the point (0,0) and you can cut off the tree in (0,0) directly without walking.
```
 
**Constraints:**

* `1 <= forest.length <= 50`
* `1 <= forest[i].length <= 50`
* `0 <= forest[i][j] <= 10^9`

**Code:**

```python
from collections import deque
class Solution:
    def cutOffTree(self, forest: List[List[int]]) -> int:
        M, N = len(forest), len(forest[0])
        trees = []
        for i in range(M):
            for j in range(N):
                if forest[i][j] > 1:
                    trees.append((forest[i][j], i, j))
        trees.sort()
        cnt = 0
        curr_i, curr_j = 0, 0
        
        def dist(ci, cj, ni, nj):
            queue = deque([(ci, cj, 0)])
            seen = {(ci, cj)}
            while queue:
                i, j, d = queue.pop()
                if (i, j) == (ni, nj):
                    return d
                for dx, dy in [[0, 1], [1, 0], [-1, 0], [0, -1]]:
                    x, y = i + dx, j + dy
                    if 0 <= x < M and 0 <= y < N and forest[x][y] > 0 and (x, y) not in seen:
                        seen.add((x, y))
                        queue.appendleft((x, y, d + 1))
            return -1
        
        for i in range(len(trees)):
            next_i, next_j = trees[i][1:]
            d = dist(curr_i, curr_j, next_i, next_j)
            if d == -1:
                return -1
            cnt += d
            curr_i, curr_j = next_i, next_j
        return cnt
```
sort the trees by height and than loop througth the trees, use bfs to get the distance between two trees.
