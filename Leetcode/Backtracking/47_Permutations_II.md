## Link
```
Given a collection of numbers that might contain duplicates, return all possible unique permutations.

Example:

Input: [1,1,2]
Output:
[
  [1,1,2],
  [1,2,1],
  [2,1,1]
]
```
## Solution
1. Base case
2. DFS
```python
class Solution:
    def permuteUnique(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        res = []
        if len(nums) == 0:
            return []
        if len(nums) == 1:
            return [nums]
        
        for i in range(len(nums)):
            pre = nums[i]
            rest = nums[:i] + nums[i+1:]
            for j in self.permuteUnique(rest):
                if [pre]+j not in res:
                    res.append([pre] + j)
        return res 
```
