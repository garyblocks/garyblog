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
        N = len(height)
        if N < 1:
            return 0
        l, r = 0, N - 1
        max_area = 0
        while l <= r:
            area = (r - l) * min(height[l], height[r])
            max_area = max(area, max_area)
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return max_area
```
#### Idea:
Use **two pointers** moving towards each other, always move the pointer with the shorter height.

#### Explanation:
To understand this, the area is calculated as the product of width and min height of two bars, we start with the largest width, so the only way to increase the  area is to have a higher min bar height, and that can only be achieved by move the pointer on the shorter bar to find a higher one. And this is true for each step.

Are we going to miss anything? No, because the areas we didn't check are those infront of the taller bar. Since the shorter bar defines the min height, the only chance to be better is a larger width, but they will never have a width wider than the current taller bar as they are in front of it. So we won't miss a bigger area.

#### Complexity:
* Space: \\( O(1) \\)
* Time: \\( O(N) \\)
