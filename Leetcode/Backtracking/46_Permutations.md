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
- Time O(n * n!), space O(n * n!)
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
### DFS2
```python
# DFS
def permute(self, nums):
    res = []
    self.dfs(nums, [], res)
    return res
    
def dfs(self, nums, path, res):
    if not nums:
        res.append(path)
        # return # backtracking
    for i in xrange(len(nums)):
        self.dfs(nums[:i]+nums[i+1:], path+[nums[i]], res)
```
### Iterative

the basic idea is, to permute n numbers, we can add the nth number into the resulting List<List<Integer>> from the n-1 numbers, in every possible position.

For example, if the input num[] is {1,2,3}: First, add 1 into the initial List<List<Integer>> (let's call it "answer").

Then, 2 can be added in front or after 1. So we have to copy the List in answer (it's just {1}), add 2 in position 0 of {1}, then copy the original {1} again, and add 2 in position 1. Now we have an answer of {{2,1},{1,2}}. There are 2 lists in the current answer.

Then we have to add 3. first copy {2,1} and {1,2}, add 3 in position 0; then copy {2,1} and {1,2}, and add 3 into position 1, then do the same thing for position 3. Finally we have 2*3=6 lists in answer, which is what we want.
```
class Solution:
    def permute(self, nums):
        """
        :type nums: List[int]
        :rtype: List[List[int]]
        """
        perms = [[]]
        for n in nums:
            new_perms = []
            for perm in perms:
                for i in range(len(perm)+1):
                    new_perms.append(perm[:i] + [n] + perm[i:])
            perms = new_perms
        return perms
```
