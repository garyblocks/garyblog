## Trapping Rain Water
Given n non-negative integers representing an elevation map where the width of each bar is 1, compute how much water it is able to trap after raining.

**Example:**

```
Input: [0,1,0,2,1,0,1,3,2,1,2,1]
Output: 6
```

**Code:**

```
def trap(self, height):
    decreasingHeightStack, totalWaterTrapped = [], 0
    for i, v in enumerate(height):
        while len(decreasingHeightStack) > 0 and height[decreasingHeightStack[-1]] < v:
            bottomHeight = height[decreasingHeightStack.pop()]
            if len(decreasingHeightStack) == 0:
                break
            leftUpperIndex = decreasingHeightStack[-1]
            heightDiff = min(height[leftUpperIndex], v) - bottomHeight
            width = i - leftUpperIndex - 1
            totalWaterTrapped += heightDiff * width
            
        decreasingHeightStack.append(i)
        
    return totalWaterTrapped
```

