# Insert Interval

Given a set of non-overlapping intervals, insert a new interval into the intervals (merge if necessary).

You may assume that the intervals were initially sorted according to their start times.

**Example:**

```
Input: intervals = [[1,3],[6,9]], newInterval = [2,5]
Output: [[1,5],[6,9]]
```
```
Input: intervals = [[1,2],[3,5],[6,7],[8,10],[12,16]], newInterval = [4,8]
Output: [[1,2],[3,10],[12,16]]
Explanation: Because the new interval [4,8] overlaps with [3,5],[6,7],[8,10].
```

**Code:**

```python
class Solution:
    def insert(self, intervals: List[List[int]], newInterval: List[int]) -> List[List[int]]:
        if not intervals:
            return [newInterval]
        N = len(intervals)
        ret = []
        i = 0
        while i < N:
            intv = intervals[i]
            if intv[0] < newInterval[0]:
                ret.append(intv)
            else:
                break
            i += 1
        if not ret or newInterval[0] > ret[-1][1]:
            ret.append(newInterval)
        else:
            ret[-1][1] = max(newInterval[1], ret[-1][1])
        while i < N:
            intv = intervals[i]
            if intv[0] > ret[-1][1]:
                ret.append(intv)
            else:
                ret[-1][1] = max(intv[1], ret[-1][1])
            i += 1
        return ret
```

pass everything before, then add new interval, finally merge the rest in.
