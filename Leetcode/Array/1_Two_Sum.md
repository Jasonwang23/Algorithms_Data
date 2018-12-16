## Link

https://leetcode.com/problems/two-sum/

```
Given an array of integers, 
return indices of the two numbers such that they add up to a specific target.
You may assume that each input would have exactly one solution, 
and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,

return [0, 1].
```

## 解题思路
### BT
两轮遍历
- Time O(n^2), Space O(1)

```python
class Solution(object):
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i, j]
```
### Hashtable
1. 创建一个hashtable，key is index i, value is nums[i] --> {nums[i]:i}
2. loop the array, set com to (target - nums[i]), if com is in the hashtable, return two indexes of array
3. else, put i into the hashtable
- Time O(n), Space O(n)
```python
class Solution:
    def twoSum(self, nums, target):
        """
        :type nums: List[int]
        :type target: int
        :rtype: List[int]
        """
        if len(nums) <= 1:
            return False
        
        my_dict = {}
        for i in range(len(nums)):
            com = target - nums[i]
            if com in my_dict:
                return [my_dict[com], i]
            else:
                my_dict[nums[i]] = i
            
```
