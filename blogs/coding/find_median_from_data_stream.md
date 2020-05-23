# Find Median from Data Stream

Median is the middle value in an ordered integer list. If the size of the list is even, there is no middle value. So the median is the mean of the two middle value.

For example,
`[2,3,4]`, the median is `3`

`[2,3]`, the median is `(2 + 3) / 2 = 2.5`

Design a data structure that supports the following two operations:

* void addNum(int num) - Add a integer number from the data stream to the data structure.
* double findMedian() - Return the median of all elements so far.
 

**Example:**

```
addNum(1)
addNum(2)
findMedian() -> 1.5
addNum(3) 
findMedian() -> 2
```
 

Follow up:

* If all integer numbers from the stream are between 0 and 100, how would you optimize it?
* If 99% of all integer numbers from the stream are between 0 and 100, how would you optimize it?

**Code:**

```python
import heapq as hq

class MedianFinder:

    def __init__(self):
        self.small_heap = []
        self.large_heap = []
        self.med = 0.0
        

    def addNum(self, num: int) -> None:
        if not self.small_heap:
            hq.heappush(self.small_heap, -num)
            self.med = num
            return
        if num > -self.small_heap[0]:
            hq.heappush(self.large_heap, num)
            if len(self.large_heap) > len(self.small_heap):
                large_min = hq.heappop(self.large_heap)
                hq.heappush(self.small_heap, -large_min)
                self.med = large_min
            else:
                self.med = (-self.small_heap[0] + self.large_heap[0]) / 2
        else:
            hq.heappush(self.small_heap, -num)
            if len(self.small_heap) > len(self.large_heap) + 1:
                small_max = -hq.heappop(self.small_heap)
                hq.heappush(self.large_heap, small_max)
                self.med = (-self.small_heap[0] + small_max) / 2
            else:
                self.med = -self.small_heap[0]
                

    def findMedian(self) -> float:
        return self.med
```
Use two heaps, keep balancing the heap sizes to let median be one of the tips.