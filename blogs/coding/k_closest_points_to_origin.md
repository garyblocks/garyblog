## K Closest Points to Origin
We have a list of `points` on the plane.  Find the `K` closest points to the origin `(0, 0)`.

(Here, the distance between two points on a plane is the Euclidean distance.)

You may return the answer in any order.  The answer is guaranteed to be unique (except for the order that it is in.)

**Example:**

```
Input: points = [[1,3],[-2,2]], K = 1
Output: [[-2,2]]
Explanation: 
The distance between (1, 3) and the origin is sqrt(10).
The distance between (-2, 2) and the origin is sqrt(8).
Since sqrt(8) < sqrt(10), (-2, 2) is closer to the origin.
We only want the closest K = 1 points from the origin, so the answer is just [[-2,2]].
```
```
Input: points = [[3,3],[5,-1],[-2,4]], K = 2
Output: [[3,3],[-2,4]]
(The answer [[-2,4],[3,3]] would also be accepted.)
```

**Note:**

* `1 <= K <= points.length <= 10000`
* `-10000 < points[i][0] < 10000`
* `-10000 < points[i][1] < 10000`

**Code:**

```python
from random import randint
class Solution:
    def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        def dist(p):
            return p[0]*p[0] + p[1]*p[1]
        
        def partition(l, h):
            r = randint(l, h)
            pivot = dist(points[r])
            points[h], points[r] = points[r], points[h]
            j = l-1
            for i in range(l, h):
                if dist(points[i]) < pivot:
                    j += 1
                    points[j], points[i] = points[i], points[j]
            points[j+1], points[h] = points[h], points[j+1]
            return j + 1
        
        if K == 0 or len(points) < K:
            return []
        
        l, h = 0, len(points) - 1
        while l < h:
            p = partition(l, h)
            if p == K - 1:
                break
            elif p > K - 1:
                h = p-1
            else:
                l = p+1
        return points[:K]
```
We take advantage of return K not in order, use quick sort to partial sort the array. Recursively find a random point, make sure the elements on its left are smaller than the ones on its right, until we find the first K elements. Return them. We only do at most N switches, so it's O(N) time complexity.
