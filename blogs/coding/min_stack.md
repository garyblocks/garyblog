## Min Stack

Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.

* push(x) -- Push element x onto stack.
* pop() -- Removes the element on top of the stack.
* top() -- Get the top element.
* getMin() -- Retrieve the minimum element in the stack.

**Example:**

```
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin();   --> Returns -3.
minStack.pop();
minStack.top();      --> Returns 0.
minStack.getMin();   --> Returns -2.
```

**Code:**

```python
class MinStack:

    def __init__(self):
        self.array = []

    def push(self, x: int) -> None:
        if not self.array:
            self.array.append((x, x))
        else:
            self.array.append((x, min(x, self.array[-1][1])))

    def pop(self) -> None:
        self.array.pop()

    def top(self) -> int:
        return self.array[-1][0]

    def getMin(self) -> int:
        return self.array[-1][1]

```
Since the minimum of numbers that are already in the stack is never going to change until they got popped out, we can save the minimum along side the numers in a list, and then just implement the regurlar stack.