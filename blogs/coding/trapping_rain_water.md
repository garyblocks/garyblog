## Trapping Rain Water
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

**Code:**

```python
class Solution:
    def trap(self, height: List[int]) -> int:
        stack = []
        ret = 0
        for i, h in enumerate(height):
            while stack and h >= height[stack[-1]]:
                curr = stack.pop()
                if stack:
                    boundary = min(height[stack[-1]], h)
                    ret += (boundary - height[curr]) * (i - stack[-1] - 1)
            stack.append(i)
        return ret
```
#### Idea
Use a monotonic stack to save the left boundaries.

