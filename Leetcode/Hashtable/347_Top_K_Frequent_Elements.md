## Link
https://leetcode.com/problems/top-k-frequent-elements/
```
Given a non-empty array of integers, return the k most frequent elements.

Example 1:

Input: nums = [1,1,1,2,2,3], k = 2
Output: [1,2]
Example 2:

Input: nums = [1], k = 1
Output: [1]
Note:

You may assume k is always valid, 1 ≤ k ≤ number of unique elements.
Your algorithm's time complexity must be better than O(n log n), where n is the array's size.

```
## Solution
1. build a hashtable, {num:frequency}
2. build a list(bucket), index: frequency, value: num
3. get top k element from bucket
- Time O(n), space O(n)
![Image of code](http://zxi.mytechroad.com/blog/wp-content/uploads/2017/10/347-ep95.png)
```python
class Solution:
    def topKFrequent(self, nums, k):
        """
        :type nums: List[int]
        :type k: int
        :rtype: List[int]
        """
        d = {}
        for num in nums:
            d[num] = d.get(num, 0) + 1
        
        bucket = [[] for _ in range(len(nums) + 1)]
        for num in d.keys():
            bucket[d[num]].append(num)
            
        ans = []
        for i in range(len(nums), 0 ,-1):
            ans += (bucket[i])
            if len(ans) == k:
                return ans
```
