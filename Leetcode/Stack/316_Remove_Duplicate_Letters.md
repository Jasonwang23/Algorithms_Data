## Link
https://leetcode.com/problems/remove-duplicate-letters/

https://docs.python.org/2/library/collections.html

```
Given a string which contains only lowercase letters, 
remove duplicate letters so that every letter appear once and only once. You must make sure your result is the smallest in lexicographical order among all possible results.

Example 1:

Input: "bcabc"
Output: "abc"
Example 2:

Input: "cbacdcbc"
Output: "acdb"
```
## Solution
- Use a hastable to count the number of characters in the string

for every character in the string, if it's not in the res
1. if res[-1] > c and count > 0, then delete it from res
2. if it's in the res, reduce the count
```python
import collections
class Solution:
    def removeDuplicateLetters(self, s):
        """
        :type s: str
        :rtype: str
        """
        count = collections.defaultdict(int)
        for c in s:
            count[c] += 1
        res = []
        
        for c in s:
            if c not in res:
                while res and res[-1] > c and count[res[-1]] > 0:
                    res.pop()
                res.append(c)
            count[c] -= 1
                
        return ''.join(res)
```
