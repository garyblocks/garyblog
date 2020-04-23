## Median of Two Sorted Arrays

There are two sorted arrays `nums1` and `nums2` of size m and `n` respectively.

Find the median of the two sorted arrays. The overall run time complexity should be `O(log (m+n))`.

You may assume `nums1` and `nums2` cannot be both empty.

**Example:**

```
nums1 = [1, 3]
nums2 = [2]

The median is 2.0
```
```
nums1 = [1, 2]
nums2 = [3, 4]

The median is (2 + 3)/2 = 2.5
```

**Code:**

```python
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        l1, l2 = len(nums1), len(nums2)  
        if l1 > l2:
            # here we want to make sure nums is shorter
            # as we are calculating index on nums2 by substracting index on nums1
            # otherwise, the index could be negative
            return self.findMedianSortedArrays(nums2, nums1)
        imin, imax, mid = 0, l1, (l1 + l2 + 1) // 2
        while imin <= imax:
            i = (imin + imax) // 2
            j = mid - i
            if j > 0 and i < l1 and nums2[j - 1] > nums1[i]:
                imin = i + 1
            elif i > 0 and j < l2 and nums1[i - 1] > nums2[j]:
                imax = i - 1
            else:
                if i == 0:
                    max_left = nums2[j-1]
                elif j == 0:  # need this in case the lens are the same
                    max_left = nums1[i-1]
                else:
                    max_left = max(nums1[i-1], nums2[j-1])
                if (l1 + l2) % 2:
                    return max_left
                
                if i == l1:
                    min_right = nums2[j]
                elif j == l2:
                    min_right = nums1[i]
                else:
                    min_right = min(nums1[i], nums2[j])
                return (max_left + min_right) / 2.0
```
The general idea is to find two cuts on these two arrays that can split each of them into two subarrays, and all the elements on the right of these cuts are larger than the ones on the left, and there are same amount of elements on each side.

Once we have a pair of cuts like that, than we can find the median around these cuts. To keep the sizes of both sides equal, we only search for one cut and calcuate the other by array size. That's where i and j are related.

The search process is a binary search, we want to search only on the shorter array to make sure the other index is positive. For each step, we check if the left edges are smaller than the right edges, if so, we move the cut to right and vice versa.

Finally, we deal with the edges cases and the odd/even issues.