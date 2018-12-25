## Link
https://leetcode.com/problems/longest-palindromic-substring/
```
Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"
```
## Solution
### Longest common substring 
- LCSuff(S1...p, T1...q) = LCS(S1...p1, T1...q-1) if S[p] = T[q] else 0
![Image of code](https://github.com/Jasonwang23/Algorithms_Data/blob/master/Pics/453651CE-B839-4DC8-8535-5B239E5B5CD4.png)
```python
class Solution(object):
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        def lcs(s1, s2):
            m = [[0] * (1 + len(s2)) for i in xrange(1 + len(s1))]
            longest, x_longest = 0, 0
            for x in xrange(1, 1 + len(s1)):
                for y in xrange(1, 1 + len(s2)):
                    if s1[x - 1] == s2[y - 1]:
                        m[x][y] = m[x - 1][y - 1] + 1
                        if m[x][y] > longest:
                            longest = m[x][y]
                            x_longest = x
                    else:
                        m[x][y] = 0
            return s1[x_longest - longest: x_longest]

        return lcs(s, s[::-1])
```







```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        ans=''
        n = len(s)
        for i in range(n):
            
            temp = self.helper(s,i,i)
            if len(temp) > len(ans):
                ans = temp
            
            temp = self.helper(s,i,i+1)
            if len(temp) > len(ans):
                ans = temp
        return ans
        
        
    def helper(self, s, l, r):
        while l>=0 and r < len(s) and s[l] == s[r]:
            l -= 1
            r += 1
        return s[l+1:r]
```
