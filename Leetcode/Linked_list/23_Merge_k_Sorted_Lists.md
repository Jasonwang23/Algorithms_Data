## Link
https://leetcode.com/problems/merge-k-sorted-lists/
```
Merge k sorted linked lists and return it as one sorted list. Analyze and describe its complexity.

Example:

Input:
[
  1->4->5,
  1->3->4,
  2->6
]
Output: 1->1->2->3->4->4->5->6
```
## Solution
### Priority queue
- Compare the fist node of each linked list, if it's samller than the other, and then get the next node of this linked list and then continue to compare
- Time O(nlogk), space O(n)
1. Put first val and node of every linked list into priority queue
2. Get the first val and node in the priority queue and add to the new linked list
3. Keep get the next node from current node
```python
# Definition for singly-linked list.
# class ListNode(object):
#     def __init__(self, x):
#         self.val = x
#         self.next = None

from Queue import PriorityQueue
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        q = PriorityQueue()
        head = point = ListNode(0)
        for l in lists:
            if l:
                q.put((l.val, l))
        while not q.empty():
            val, node = q.get()
            point.next = ListNode(val)
            point = point.next
            node = node.next
            if node:
                q.put((node.val, node))
        return head.next
```
```python
#python 3
import heapq
import collections
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        heap = []
        d = collections.defaultdict(list)
        head = cur = ListNode(0)
        for l in lists:
            if l:
                heapq.heappush(heap, l.val)
                d[l.val].append(l)
                
        while heap:
            val = heapq.heappop(heap)
            node = d[val].pop(0)
            cur.next = ListNode(val)
            cur = cur.next
            node = node.next
            if node:
                heapq.heappush(heap, node.val)
                d[node.val].append(node)
        return head.next
```
### Divide and conquer
```
class Solution(object):
    def mergeKLists(self, lists):
        """
        :type lists: List[ListNode]
        :rtype: ListNode
        """
        if not lists:
            return 
        if len(lists) == 1:
            return lists[0]
        mid = len(lists)//2
        l = self.mergeKLists(lists[:mid])
        r = self.mergeKLists(lists[mid:])
        return self.merge(l,r)
    
    def merge(self, l, r):
        head = cur = ListNode(0)
        while l and r:
            if l.val < r.val:
                cur.next = l
                l = l.next
            else:
                cur.next = r
                r = r.next
            cur = cur.next
        cur.next = l or r
        return head.next
```
