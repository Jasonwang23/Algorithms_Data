## Link
https://leetcode.com/problems/valid-parentheses/
```
Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

An input string is valid if:

Open brackets must be closed by the same type of brackets.
Open brackets must be closed in the correct order.
Note that an empty string is also considered valid.

Example 1:

Input: "()"
Output: true
Example 2:

Input: "()[]{}"
Output: true
Example 3:

Input: "(]"
Output: false
Example 4:

Input: "([)]"
Output: false
Example 5:

Input: "{[]}"
Output: true
```
## Solution
```python
class Solution:
    def isValid(self, s):
        """
        :type s: str
        :rtype: bool
        """
        p = []
        d = {')':'(', '}':'{', ']':'['}
        for char in s:
            if char in d.values():
                p.append(char)
            elif char in d.keys():
                if len(p) == 0:
                    return False
                elif p.pop() != d[char]:
                    return False
        
        return len(p) == 0
```
