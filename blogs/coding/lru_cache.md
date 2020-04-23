## LRU Cache

Design and implement a data structure for Least Recently Used (LRU) cache. It should support the following operations: `get` and `put`.

`get(key)` - Get the value (will always be positive) of the key if the key exists in the cache, otherwise return -1.
`put(key, value)` - Set or insert the value if the key is not already present. When the cache reached its capacity, it should invalidate the least recently used item before inserting a new item.

The cache is initialized with a *positive* capacity.

*Follow up:*
Could you do both operations in *O(1)* time complexity?

**Example:**

```
LRUCache cache = new LRUCache( 2 /* capacity */ );

cache.put(1, 1);
cache.put(2, 2);
cache.get(1);       // returns 1
cache.put(3, 3);    // evicts key 2
cache.get(2);       // returns -1 (not found)
cache.put(4, 4);    // evicts key 1
cache.get(1);       // returns -1 (not found)
cache.get(3);       // returns 3
cache.get(4);       // returns 4
```
**Code:**

```python
from collections import OrderedDict
class LRUCache:

    def __init__(self, capacity: int):
        self.values = OrderedDict()
        self.N = capacity

    def get(self, key: int) -> int:
        if key in self.values:
            value = self.values.pop(key)
            self.values[key] = value
            return self.values[key]
        else:
            return -1

    def put(self, key: int, value: int) -> None:
        if key in self.values:
            self.values.pop(key)
        elif len(self.values) == self.N:
            self.values.popitem(last=False)
        self.values[key] = value
```
We need a dictionary to quick access and remove the data and we also need a list to remember the order. The list has to be a double linked list so we can do remove in O(1) time. In python OrderedDict is a combination of both, we can just use it to solve the problem.