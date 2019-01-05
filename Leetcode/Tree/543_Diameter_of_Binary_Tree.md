## Link
https://leetcode.com/problems/diameter-of-binary-tree/
```
Given a binary tree, you need to compute the length of the diameter of the tree. 
The diameter of a binary tree is the length of the longest path between any two nodes in a tree. This path may or may not pass through the root.

Example:
Given a binary tree 
          1
         / \
        2   3
       / \     
      4   5    
Return 3, which is the length of the path [4,2,1,3] or [5,2,1,3].

Note: The length of path between two nodes is represented by the number of edges between them.
```
## Solution
1. Diameter = maximum length arrows L, R for each child, then the best path touches L + R + 1 nodes 
2. Calculate the depth of a node in the usual way: max(depth of node.left, depth of node.right) + 1
- Time O(n), space O(n)
```python
# Definition for a binary tree node.
# class TreeNode:
#     def __init__(self, x):
#         self.val = x
#         self.left = None
#         self.right = None

class Solution:
    def diameterOfBinaryTree(self, root):
        """
        :type root: TreeNode
        :rtype: int
        """
        self.ans = 0
        
        def depth(p):
            if not p:
                return 0
            l = depth(p.left)
            r = depth(p.right)
            self.ans = max(self.ans, l+r)
            return 1 + max(l, r)
        
        depth(root)
        return self.ans
```
