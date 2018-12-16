## Link
https://leetcode.com/problems/group-anagrams/
```
Given an array of strings, group anagrams together.

Example:

Input: ["eat", "tea", "tan", "ate", "nat", "bat"],
Output:
[
  ["ate","eat","tea"],
  ["nat","tan"],
  ["bat"]
]
Note:

All inputs will be in lowercase.
The order of your output does not matter.
```
## Solution
- Time O(NKlongK), Space O(NK)
N is length of list, K is max length of string in strs
1. Sort each str and save to a tuple to be the key(key should be unchanged)
2. Create a empty list for each key, append corresponding str to the list
```python
class Solution:
    def groupAnagrams(self, strs):
        """
        :type strs: List[str]
        :rtype: List[List[str]]
        """
        d = {}
        if strs is None or len(strs) == 0:
            return[[]]
        
        for s in strs:
            s_sort = sorted(s)
            s_key = tuple(s_sort)
            
            d[s_key] = d.get(s_key, [])
            d[s_key].append(s)
            
        return list(d.values())
```
