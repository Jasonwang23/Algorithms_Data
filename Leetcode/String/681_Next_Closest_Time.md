## Link
https://leetcode.com/problems/next-closest-time/
```
Given a time represented in the format "HH:MM", form the next closest time by reusing the current digits. There is no limit on how many times a digit can be reused.

You may assume the given input string is always valid. For example, "01:34", "12:09" are all valid. "1:34", "12:9" are all invalid.

Example 1:

Input: "19:34"
Output: "19:39"
Explanation: The next closest time choosing from digits 1, 9, 3, 4, is 19:39, which occurs 5 minutes later.  It is not 19:33, because this occurs 23 hours and 59 minutes later.
Example 2:

Input: "23:59"
Output: "22:22"
Explanation: The next closest time choosing from digits 2, 3, 5, 9, is 22:22. It may be assumed that the returned time is next day's time since it is smaller than the input time numerically.
```
## Solution
1. Simulate the clock going 1 minute each time, try all the time to the next day, if all the digits are allowed,
return the current time
2. set compare if set A in set B, A <= B
- Python
https://www.programiz.com/python-programming/methods/string/format
http://www.runoob.com/python/att-string-format.html
- set compare
https://www.linuxtopia.org/online_books/programming_books/python_programming/python_ch16s04.html
- Time O(1), space O(1)
```python
class Solution:
    def nextClosestTime(self, time):
        """
        :type time: str
        :rtype: str
        """
        h, m = time.split(":")
        cur = int(h)*60 + int(m)
        for i in range(1, 1441):
            t = (cur + i) % 1440
            h, m = t//60, t%60
            result = "%02d:%02d" % (h,m)
            if set(result) <= set(time):
                break
        return result
```

