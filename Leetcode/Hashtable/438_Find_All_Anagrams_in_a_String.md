## Link 
https://leetcode.com/problems/find-all-anagrams-in-a-string/
```
Given a string s and a non-empty string p, find all the start indices of p's anagrams in s.

Strings consists of lowercase English letters only and the length of both strings s and p 
will not be larger than 20,100.

The order of output does not matter.

Example 1:

Input:
s: "cbaebabacd" p: "abc"

Output:
[0, 6]

Explanation:
The substring with start index = 0 is "cba", which is an anagram of "abc".
The substring with start index = 6 is "bac", which is an anagram of "abc".
Example 2:

Input:
s: "abab" p: "ab"

Output:
[0, 1, 2]

Explanation:
The substring with start index = 0 is "ab", which is an anagram of "ab".
The substring with start index = 1 is "ba", which is an anagram of "ab".
The substring with start index = 2 is "ab", which is an anagram of "ab".
```
## Solution
1. build a hashtable to store {character:freqs}, and a counter to count the number of character 
that freqs is not or less than 0
2. move end
3. While counter = 0, if end - begin = len(p), return begin, if s[begin] in maps, update maps nad counter
```python
import collections
class Solution:
    def findAnagrams(self, s, p):
        """
        :type s: str
        :type p: str
        :rtype: List[int]
        """
        ans = []
        end, begin = 0,0
        maps = collections.Counter(p)
        counter = len(maps.keys())
        while end < len(s):
            if s[end] in maps:
                maps[s[end]] -= 1
                if maps[s[end]] == 0:
                    counter -= 1
            end += 1
            
            while counter == 0:
                if end - begin == len(p):
                    ans.append(begin)
                if s[begin] in maps:
                    maps[s[begin]] += 1
                    if maps[s[begin]] == 1:
                        counter += 1
                begin += 1
        return ans
```
