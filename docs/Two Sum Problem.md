# Two Sum

## Notes
- LeetCode problem: [Two Sum](https://leetcode.com/problems/two-sum/)
- Difficulty: Easy
- Topics: Array, Hash Table, Two Pointers

## Description
Given an array of integers `nums` and an integer `target`, return indices of the two numbers such that they add up to `target`. Each input has exactly one solution, and you may not use the same element twice.

**Example:**
```
Input: nums = [2,7,11,15], target = 9
Output: [0,1]
```

## Python3 Solutions
### Brute Force (O(n²))
```python
from typing import List
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        n = len(nums)
        for i in range(n):
            for j in range(i+1, n):
                if nums[i] + nums[j] == target:
                    return [i, j]
```
### Hash Map (O(n))
```python
from typing import List
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        lookup = {}
        for i, num in enumerate(nums):
            complement = target - num
            if complement in lookup:
                return [lookup[complement], i]
            lookup[num] = i
```
## Go Solutions
### Brute Force (O(n²))
```go
func twoSum(nums []int, target int) []int {
    for i := 0; i < len(nums); i++ {
        for j := i + 1; j < len(nums); j++ {
            if nums[i]+nums[j] == target {
                return []int{i, j}
            }
        }
    }
    return nil
}
```
### Hash Map (O(n))
```go
func twoSum(nums []int, target int) []int {
    lookup := make(map[int]int)
    for i, num := range nums {
        if j, ok := lookup[target-num]; ok {
            return []int{j, i}
        }
        lookup[num] = i
    }
    return nil
}
```
## References
- LeetCode official solution: https://leetcode.com/problems/two-sum/solutions/
- GeeksforGeeks article: https://www.geeksforgeeks.org/2sum-array-two-pointer-technique/
- YouTube tutorial: https://youtu.be/7y5J0lRzVgY
