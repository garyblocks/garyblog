## Load Balancer
Write a function solution that, given an array A of N integers representing the time of execution of consecutive tasks, returns true if it is possible for the load balancer to choose two requests that will determine an even distribution of requests among three workers, or false otherwise.

**Examples:**

```
Input: A = [1, 3, 4, 2, 2, 2, 1, 1, 2],
Output: true
Explanation: as choosing requests 2 and 5 results in a distribution giving 4 seconds of handling time to each worker.
```
```
Input: A = [1, 1, 1, 1, 1, 1],
Output: false.
```
```
Input: A = [1, 2, 1, 2, ..., 1, 2] of length 20,000,
Output: true.
```
**Notes:**

* N is an integer within the range [5..100,000];
* each element of array A is an integer within the range [1..10,000].

**Code:**

```
def balancing_possible(nums):
    if len(nums) < 5:
        return False
    total_sum = sum(nums)
    left_index, right_index = 1, len(nums) - 2
    left_sum, right_sum = nums[0], nums[-1]
    
    while left_index < right_index:
        drop_sum = nums[left_index] + nums[right_index]
        mid_sum = total_sum - drop_sum - left_sum - right_sum
        
        if mid_sum < left_sum or mid_sum < right_sum:
            return False
        if left_sum == mid_sum == right_sum:
            return True
        
        if left_sum <= right_sum:
            left_sum += nums[left_index]
            left_index += 1
        else:
            right_sum += nums[right_index]
            right_index -= 1
    
    return False
```

