# Meeting Rooms II

Given an array of meeting time intervals consisting of start and end times `[[s1,e1],[s2,e2],...]` \\((s_i < e_i)\\), find the minimum number of conference rooms required.

**Example:**

```
Input: [[0, 30],[5, 10],[15, 20]]
Output: 2
```
```
Input: [[7,10],[2,4]]
Output: 1
```

**NOTE:** input types have been changed on April 15, 2019. Please reset to default code definition to get new method signature.

**Code:**

```python
class Solution:
    def minMeetingRooms(self, intervals: List[List[int]]) -> int:
        points = []
        for i, intv in enumerate(intervals):
            start, end = intv
            points.extend([(start, 1, i), (end, 0, i)])
        points = sorted(points)
        stack = set()
        rooms = 0
        for time, is_start, i in points:
            if is_start:
                stack.add(i)
                rooms = max(rooms, len(stack))
            else:
                stack.remove(i)
        return rooms
```
split the start and end time of the meetings and sort. be careful to let end come first for cases like `[1, 13], [13, 14]`