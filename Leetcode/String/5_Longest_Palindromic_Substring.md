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
1. LCSuff(S1...p, T1...q) = LCS(S1...p-1, T1...q-1) if S[p] = T[q] else 0
2. 这个方法是buggy的，看字符串abcxgcba,它reverse之后是abcgxcba,它们有公共字符串，但是这里面没有回文，修复方式是：
```
we check if the substring’s indices are the same as the reversed substring’s original indices. If it is, then we attempt to update the longest palindrome found so far; if not, we skip this and find the next candidate.

我觉得的修复方式这样么：

原本     翻转
ABXYBA   ABYXBA

求出来的substring indices是 0:2 但是这个s1[0:2] 和 s2[0:2]一样，所以不行
同理common substring indices还是s[4:6] 和s2[4:6]一样，不行

而比如ABAD和 DABA

substring indice 一个是0：3， 一个是1:4，这样就没问题
```
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
### From middle to two ends
1. Define a helper function, take every character as the middle of the palindromic-substring
2. Consider two cases, even and odd
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
### DP
https://leetcode.com/articles/longest-palindromic-substring/
1. Find transfer function and base case
```
P(i,j) = True if Si...Sj is palindrom,
esle False

Base case:
P(i,i) = True
P(i,i+1) = (Si==Si+1)

Transfer function:
P(i,j) = P(i+1,j-1) and Si == Sj
```
```python
class Solution:
    def longestPalindrome(self, s):
        """
        :type s: str
        :rtype: str
        """
        ans = ''
        n = len(s)
        max_len = 0
        dp = [[0]*n for i in range(n)]
        
        for i in range(n):
            dp[i][i] = True
            ans = s[i]
            max_len = 1
            
        for i in range(n-1):
            if s[i] == s[i+1]:
                dp[i][i+1] = True
                ans = s[i:i+2]
                max_len = 2
        
        for j in range(n):
            for i in range(j-1):
                if s[i] == s[j] and dp[i+1][j-1]:
                    dp[i][j] = True
                    if max_len < j-i+1:
                        ans = s[i:j+1]
                        max_len = j-i+1
        return ans
        
```
