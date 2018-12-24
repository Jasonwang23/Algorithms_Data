## Link
https://leetcode.com/problems/longest-substring-without-repeating-characters/
```
3. Longest Substring Without Repeating Character

Given a string, find the length of the longest substring without repeating characters.

Example 1:

Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3. 
Example 2:

Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.
Example 3:

Input: "pwwkew"
Output: 3
Explanation: The answer is "wke", with the length of 3. 
             Note that the answer must be a substring, "pwke" is a subsequence and not a substring.
```
## Solution
1. Keep a hashtable that stores characters in strings as key and their positions as value, and keep two pointers define as
max substring
2. Move the right pointer to scan the string and update the hashtable
3. If the character is already in the hashtable, then move the left pointer to the right of the same character last found
- Time complexity : O(2n)=O(n). In the worst case each character will be visited twice by i and j.
- Space complexity : O(min(m,n)). Same as the previous approach. 
We need O(k) space for the sliding window, where k is the size of the Set. 
The size of the Set is upper bounded by the size of the string n and the size of the charset/alphabet m. 
```python
class Solution:
    def lengthOfLongestSubstring(self, s):
        n = len(s)
        ans = 0
        d,i,j = {},0,0
        while (i < n and j < n):
            if s[j] not in d.values():
                d[j] = s[j]
                j += 1
                ans = max(ans, j-i)
            else:
                del d[i]
                i += 1
        return ans
```
