## Link
https://leetcode.com/problems/largest-rectangle-in-histogram/

## Solution
- Time O(n), space O(n)
1. The idea is simple, use a stack to save the index of each vector entry in a ascending order; once the current entry is smaller than the one with the index s.top(), then that means the rectangle with the height height[s.top()] ends at the current position, so calculate its area and update the maximum.
```python
class Solution:
    def largestRectangleArea(self, heights):
        """
        :type heights: List[int]
        :rtype: int
        """
        heights.append(0)
        stack = [-1]
        ans = 0
        for i in range(len(heights)):
            while heights[i] < heights[stack[-1]]:
                h = heights[stack.pop()]
                w = i - stack[-1] - 1
                ans = max(ans, w*h)
            stack.append(i)
        return ans
```
