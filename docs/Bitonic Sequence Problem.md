# Longest Bitonic Subsequence

## Notes
- LeetCode problem: [Longest Bitonic Subsequence](https://leetcode.com/problems/longest-bitonic-subsequence/)
- Difficulty: Medium
- Topics: Dynamic Programming, Array

## Description
Given an array of integers, find the length of the longest subsequence that first strictly increases and then strictly decreases.

**Example:**
```
Input: [0, 8, 4, 12, 2, 10, 6, 14, 1, 9, 5, 13, 3, 11, 7, 15]
Output: 11
Explanation: One possible longest bitonic subsequence is [0, 4, 8, 12, 14, 13, 11, 9, 6, 2, 1] (length 11).
```
## Python3 Solution
```python
def longest_bitonic_subsequence(arr):
    n = len(arr)
    if n == 0:
        return 0
    # LIS ending at i
    lis = [1]*n
    for i in range(1, n):
        for j in range(i):
            if arr[i] > arr[j] and lis[i] < lis[j]+1:
                lis[i] = lis[j]+1
    # LDS starting at i
    lds = [1]*n
    for i in range(n-2, -1, -1):
        for j in range(i+1, n):
            if arr[i] > arr[j] and lds[i] < lds[j]+1:
                lds[i] = lds[j]+1
    # Combine
    max_len = 0
    for i in range(n):
        max_len = max(max_len, lis[i]+lds[i]-1)
    return max_len
```
## Go Solution
```go
func longestBitonicSubsequence(arr []int) int {
    n := len(arr)
    if n == 0 { return 0 }
    lis := make([]int, n)
    for i := range lis { lis[i] = 1 }
    for i := 1; i < n; i++ {
        for j := 0; j < i; j++ {
            if arr[i] > arr[j] && lis[i] < lis[j]+1 {
                lis[i] = lis[j] + 1
            }
        }
    }
    lds := make([]int, n)
    for i := range lds { lds[i] = 1 }
    for i := n-2; i >= 0; i-- {
        for j := i+1; j < n; j++ {
            if arr[i] > arr[j] && lds[i] < lds[j]+1 {
                lds[i] = lds[j] + 1
            }
        }
    }
    maxLen := 0
    for i := 0; i < n; i++ {
        if lis[i]+lds[i]-1 > maxLen {
            maxLen = lis[i] + lds[i] - 1
        }
    }
    return maxLen
}
```
## References
- LeetCode discussion: https://leetcode.com/problems/longest-bitonic-subsequence/solutions/
- GeeksforGeeks article: https://www.geeksforgeeks.org/longest-bitonic-subsequence/
