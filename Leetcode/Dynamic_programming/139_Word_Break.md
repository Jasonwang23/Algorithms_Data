## Link
https://leetcode.com/problems/word-break/
```
Given a non-empty string s and a dictionary wordDict containing a list of non-empty words, 
determine if s can be segmented into a space-separated sequence of one or more dictionary words.

Note:

The same word in the dictionary may be reused multiple times in the segmentation.
You may assume the dictionary does not contain duplicate words.
Example 1:

Input: s = "leetcode", wordDict = ["leet", "code"]
Output: true
Explanation: Return true because "leetcode" can be segmented as "leet code".
Example 2:

Input: s = "applepenapple", wordDict = ["apple", "pen"]
Output: true
Explanation: Return true because "applepenapple" can be segmented as "apple pen apple".
             Note that you are allowed to reuse a dictionary word.
Example 3:

Input: s = "catsandog", wordDict = ["cats", "dog", "sand", "and", "cat"]
Output: false
```
![Image of code](http://zxi.mytechroad.com/blog/wp-content/uploads/2017/09/139.png)
## Solution
- Key of DP, store the result in process
1. Build a dp array of size n+1
2. Two pointers i and j, partitioning the current string s' into s'(0,j) and s'(j+1,i)
3. dp[0] is true, since empty string is always in the dictionary, and rest of dp initialized to false
4. id dp[j] is true and dict contains s'(j+1,i), then dp[i]=true
```python
class Solution:
    def wordBreak(self, s, wordDict):
        """
        :type s: str
        :type wordDict: List[str]
        :rtype: bool
        """
        dp = [False] * (len(s)+1)
        dp[0] = True
        for i in range(1, len(s)+1):
            for j in range(0, i):
                if dp[j] and s[j:i] in wordDict:
                    dp[i] = True
                    break
        return dp[-1]
```
