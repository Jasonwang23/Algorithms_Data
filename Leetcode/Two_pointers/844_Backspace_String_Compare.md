## Link
https://leetcode.com/problems/backspace-string-compare/
```
Given two strings S and T, return if they are equal when both are typed into empty text editors. # means a backspace character.

Example 1:

Input: S = "ab#c", T = "ad#c"
Output: true
Explanation: Both S and T become "ac".
Example 2:

Input: S = "ab##", T = "c#d#"
Output: true
Explanation: Both S and T become "".
Example 3:

Input: S = "a##c", T = "#a#c"
Output: true
Explanation: Both S and T become "c".
Example 4:

Input: S = "a#c", T = "b"
Output: false
Explanation: S becomes "c" while T becomes "b".
Note:

1 <= S.length <= 200
1 <= T.length <= 200
S and T only contain lowercase letters and '#' characters.
Follow up:

Can you solve it in O(N) time and O(1) space?
```
## Solution
### Stack
1. Build a stack, and push the character in the string into the stack if the character is not #, 
if it's #, pop the character from stack
2. Compare the result of S and T
- Time O(n), space O(n)
```python
class Solution:
    def backspaceCompare(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: bool
        """
        def afterChange(s):
            ans = []
            for c in s:
                if c != '#':
                    ans.append(c)
                elif ans:
                    ans.pop()
            return ''.join(ans)
        return afterChange(S) == afterChange(T)         
```
### Two pointer
1. The idea is we first need to find the first char in each string that was not deleted and compare equality
Corner case is that the number of '#' is larger than the number of chars in front, e.g. "ab#######c" ---> "c"
So in my codes, the outter loop condition is as long as we haven't gone through both strings, 
we need to keep going. e.g. "ab#########c" vs. "a#c"
The inner loops are to find the next char after deleting.
2. There are only two cases we need to return False:
- Both pointers are at a char and these two chars are different.
- One pointer is pointing to a char but the other string has been deleted till index 0. i.e. compare a char to an empty string

- Time O(n), space O(n)
```python
class Solution:
    def backspaceCompare(self, S, T):
        """
        :type S: str
        :type T: str
        :rtype: bool
        """
        i, ps = len(S) - 1, 0
        j, pt = len(T) - 1, 0
        
        while i>=0 or j>=0:
            while i>=0:
                if S[i] == '#':
                    ps += 1
                    i -= 1
                elif ps:
                    ps -= 1
                    i -= 1
                else:
                    break
                
                
            while j>=0:
                if T[j] == '#':
                    pt += 1
                    j -= 1
                elif pt:
                    pt -= 1
                    j -= 1
                else:
                    break
            
            if (i>=0 and j >=0) and S[i] != T[j]:
                return False
            if (i<0 and j>=0) or (i>=0 and j<0):
                return False
            
            i -= 1
            j -= 1
        return True
        
```
