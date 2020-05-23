## Course Schedule
There are a total of `numCourses` courses you have to take, labeled from `0` to `numCourses-1`.

Some courses may have prerequisites, for example to take course 0 you have to first take course 1, which is expressed as a pair: `[0,1]`

Given the total number of courses and a list of prerequisite *pairs*, is it possible for you to finish all courses?

**Example:**

```
Input: numCourses = 2, prerequisites = [[1,0]]
Output: true
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0. So it is possible.
```
```
Input: numCourses = 2, prerequisites = [[1,0],[0,1]]
Output: false
Explanation: There are a total of 2 courses to take. 
             To take course 1 you should have finished course 0, and to take course 0 you should
             also have finished course 1. So it is impossible.
```

**Constraints:**

* The input prerequisites is a graph represented by a list of edges, not adjacency matrices. Read more about how a graph is represented.
* You may assume that there are no duplicate edges in the input prerequisites.
* `1 <= numCourses <= 10^5`

**Code:**

```python
from collections import defaultdict
class Solution:
    def canFinish(self, numCourses: int, prerequisites: List[List[int]]) -> bool:
        graph = defaultdict(list)
        for k, v in prerequisites:
            graph[k].append(v)
            
        def dfs(i, seen):
            if i in seen:
                return False
            if i not in graph:
                return True
            seen.add(i)
            for j in graph[i]:
                if not dfs(j, seen):
                    return False
            seen.remove(i)
            return True
            
        for i in range(numCourses):
            seen = set()
            if not dfs(i, seen):
                return False
        return True
```
backtrack each node and check for cycles.
