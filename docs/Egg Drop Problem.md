# Egg Drop

## Notes
- LeetCode problem: [Egg Dropping Puzzle](https://leetcode.com/problems/egg-dropping-puzzle/)
- Difficulty: Hard
- Topics: Dynamic Programming, Binary Search

## Description
Given `k` floors and `n` eggs, find the minimum number of trials needed in the worst case to determine from which floor an egg will break when dropped.

**Example:**
```
k = 2 (eggs)
n = 36 (floors)
Output: 8
```
## Python3 Solutions
### Dynamic Programming (O(n*k²))
```python
def eggDrop(eggs, floors):
    dp = [[0]*(floors+1) for _ in range(eggs+1)]
    for e in range(1, eggs+1):
        dp[e][0] = 0
        dp[e][1] = 1
    for f in range(1, floors+1):
        dp[1][f] = f
    for e in range(2, eggs+1):
        for f in range(2, floors+1):
            dp[e][f] = float('inf')
            for x in range(1, f+1):
                res = 1 + max(dp[e-1][x-1], dp[e][f-x])
                if res < dp[e][f]:
                    dp[e][f] = res
    return dp[eggs][floors]
```
### Recursive with Memoization (O(n*k))
```python
from functools import lru_cache
@lru_cache(None)
def eggDrop(e, f):
    if f == 0 or f == 1:
        return f
    if e == 1:
        return f
    res = float('inf')
    for x in range(1, f+1):
        res = min(res, 1 + max(eggDrop(e-1, x-1), eggDrop(e, f-x)))
    return res
```
## Go Solutions
### DP (O(n*k²))
```go
func eggDrop(eggs, floors int) int {
    dp := make([][]int, eggs+1)
    for i := range dp {
        dp[i] = make([]int, floors+1)
    }
    for e := 1; e <= eggs; e++ {
        dp[e][0], dp[e][1] = 0, 1
    }
    for f := 1; f <= floors; f++ {
        dp[1][f] = f
    }
    for e := 2; e <= eggs; e++ {
        for f := 2; f <= floors; f++ {
            dp[e][f] = int(^uint(0) >> 1) // max int
            for x := 1; x <= f; x++ {
                res := 1 + max(dp[e-1][x-1], dp[e][f-x])
                if res < dp[e][f] {
                    dp[e][f] = res
                }
            }
        }
    }
    return dp[eggs][floors]
}
func max(a, b int) int { if a > b { return a }; return b }
```
### Memoized Recursion (O(n*k))
```go
var memo map[[2]int]int
func eggDropMemo(e, f int) int {
    key := [2]int{e, f}
    if val, ok := memo[key]; ok { return val }
    if f == 0 || f == 1 { memo[key] = f; return f }
    if e == 1 { memo[key] = f; return f }
    res := int(^uint(0) >> 1)
    for x := 1; x <= f; x++ {
        temp := 1 + max(eggDropMemo(e-1, x-1), eggDropMemo(e, f-x))
        if temp < res { res = temp }
    }
    memo[key] = res
    return res
}
```
## References
- LeetCode official solution: https://leetcode.com/problems/egg-dropping-puzzle/solutions/
- GeeksforGeeks article: https://www.geeksforgeeks.org/egg-drop-problem-set-2-dp-approach/
