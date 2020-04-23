## Container With Most Water
Given n non-negative integers `a1, a2, ..., an` , where each represents a point at coordinate `(i, ai)`. n vertical lines are drawn such that the two endpoints of line i is at `(i, ai)` and `(i, 0)`. Find two lines, which together with x-axis forms a container, such that the container contains the most water.

**Note:** You may not slant the container and n is at least 2.

**Example:**

```
Input: [1,8,6,2,5,4,8,3,7]
Output: 49
```

**Code:**

```python
class Solution:
    def maxArea(self, height: List[int]) -> int:
        i, j = 0, len(height) - 1
        max_area = min(height[i], height[j]) * (j - i)
        while j > i:
            if height[i] > height[j]:
                j -= 1
            else:
                i += 1
            new_area = min(height[i], height[j]) * (j - i)
            max_area = max(max_area, new_area)
        return max_area
```
Use two pointers moving to different directions, while keep moving the pointer with the shorter height, and this will cover all the situations, and the time complexity is O(n)

To understand this, the area is width times the min height, we start with the largest width, so the only way the area is going to be higher is to have a higher min height, and that can only be achieved by lower the pointer to the shorter height. And this is true for each step.

Are we going to miss anything? No, because the areas we didn't check are those infront of the taller bar. Since the shorter bar defines the min height, the only chance to be better is a larger width, but they will never have a width wider than the current taller bar as they are in front of it. So we won't miss a bigger area.
