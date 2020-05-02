# Merge Intervals
Given a collection of intervals, merge all overlapping intervals.

**Example:**

```
Input: [[1,3],[2,6],[8,10],[15,18]]
Output: [[1,6],[8,10],[15,18]]
Explanation: Since intervals [1,3] and [2,6] overlaps, merge them into [1,6].
```
```
Input: [[1,4],[4,5]]
Output: [[1,5]]
Explanation: Intervals [1,4] and [4,5] are considered overlapping.
```

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

**Code:**

```python
class Solution:
    def merge(self, intervals: List[List[int]]) -> List[List[int]]:
        points = []
        for start, end in intervals:
            points.append((start, 0))
            points.append((end, 1))
        points.sort()
        stack = []
        ret = []
        for p in points:
            if not p[1]:
                # start
                stack.append(p[0])
            else:
                # end
                start = stack.pop()
                if not stack:
                    ret.append([start, p[0]])
        return ret
```
split the start and end point, use a stack to keep track the opening intervals, if all the openings are closed, means we are at the end of the overlappings.
