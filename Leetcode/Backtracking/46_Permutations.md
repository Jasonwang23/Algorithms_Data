## Link
https://leetcode.com/problems/permutations/
```
Given a collection of distinct integers, return all possible permutations.

Example:

Input: [1,2,3]
Output:
[
  [1,2,3],
  [1,3,2],
  [2,1,3],
  [2,3,1],
  [3,1,2],
  [3,2,1]
]
```
## Solution
### DFS
```python
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        path = []
        self.dfs(nums, path, res)
        return res
     
    def dfs(self, nums, path, res):
        if len(path) == len(nums):
            res.append(path[:])
            return
        
        for i in range(len(nums)):
            if nums[i] not in path:
                path.append(nums[i])
                self.dfs(nums, path, res)
                path.pop()
```
