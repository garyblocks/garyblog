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
import random
class Solution:
    def kClosest(self, points: List[List[int]], K: int) -> List[List[int]]:
        dist = lambda i: points[i][0]**2 + points[i][1]**2
        
        def sort(i, j, K):
            if i >= j:
                return 
            # put random element at first
            k = random.randint(i, j)
            points[i], points[k] = points[k], points[i]
            # find the mid point of i, j
            mid = partition(i, j)
            # if exact K elements on the left, no need to sort anymore 
            if K < mid - i + 1:
                # have k element on the left i to mid
                sort(i, mid - 1, K)
            elif K > mid - i + 1:
                # on right still have K - left to solve
                sort(mid + 1, j, K-(mid-i+1))
                
        def partition(i, j):
            start = i
            pivot = dist(i)
            i += 1

            while True:
                while i < j and dist(i) < pivot:
                    i += 1
                while i <= j and dist(j) >= pivot:
                    # make sure they meet if there are duplicates
                    j -= 1
                if i >= j: break
                points[i], points[j] = points[j], points[i]
            
            # put pivot element back to middle
            points[start], points[j] = points[j], points[start]
            return j

        sort(0, len(points) - 1, K)
        return points[:K]
```
We take advantage of return K not in order, use quick sort to partial sort the array. Recursively find a random point, make sure the elements on its left are smaller than the ones on its right, until we find the first K elements. Return them. We only do at most N switches, so it's O(N) time complexity.
