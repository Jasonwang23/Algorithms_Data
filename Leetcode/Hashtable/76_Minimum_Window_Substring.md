## Link
https://leetcode.com/problems/minimum-window-substring/
```
Given a string S and a string T, 
find the minimum window in S which will contain all the characters in T in complexity O(n).

Example:

Input: S = "ADOBECODEBANC", T = "ABC"
Output: "BANC"
Note:

If there is no such window in S that covers all characters in T, return the empty string "".
If there is such window, you are guaranteed that there will always be only one unique minimum window in S.
```
## Solution
1. We should have a concept of window, if end of window less than len(s), keep going. Window moves on s
2. Use a hashtable to store {character:freqs} of t, update the hashtable when end moves, if the new character is in
the hashtable, reduce the freqs in hashtable
3. Use a counter to count the number of character that freqs is not 0, If the counter
is 0, we know that all the character is in the window
4. We move the begin now, if the counter is also 0, we can keep moving beign to redece the size of window
5. When get out of the loop while end < len(s), we need to judge if the size of window is changed, if it is changed,
the return
