## Link
https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/
```
Given a string s , find the length of the longest substring t  that contains at most 2 distinct characters.

Example 1:

Input: "eceba"
Output: 3
Explanation: t is "ece" which its length is 3.
Example 2:

Input: "ccaabbb"
Output: 5
Explanation: t is "aabbb" which its length is 5.
```
## Solution
1. use two pointers begin and end, while (end < len(s)), move end on s
2. build a hashtable to store {character:freqs}, and a counter to count the number of character that freqs is not 0, 
if counter < 2: counter + 1
3. if counter > 2, move begin, if freqs of s[begin] is 0, counter - 1 
4. Out of (end < len(s)) loop, return max length
- Time O(), space O()
```python
class Solution:
    def lengthOfLongestSubstringTwoDistinct(self, s):
        """
        :type s: str
        :rtype: int
        """
        if len(s) <= 2:
            return len(s)
        maps = {}
        begin, end, counter, length = 0,0,0,0
        while end < len(s):
            maps[s[end]] = maps.get(s[end], 0) + 1
            if maps[s[end]] == 1:
                counter += 1
            end += 1
            
            while counter > 2:
                maps[s[begin]] -= 1
                if maps[s[begin]] == 0:
                    counter -= 1
                begin += 1
            length = max(length, end - begin)
                
        return length
```
## Template
https://leetcode.com/problems/longest-substring-with-at-most-two-distinct-characters/discuss/49708/Sliding-Window-algorithm-template-to-solve-all-the-Leetcode-substring-search-problem.
