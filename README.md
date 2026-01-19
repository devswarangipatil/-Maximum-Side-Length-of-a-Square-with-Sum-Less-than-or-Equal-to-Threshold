# Maximum-Side-Length-of-a-Square-with-Sum-Less-than-or-Equal-to-Threshold

Given a m x n matrix mat and an integer threshold, return the maximum side-length of a square with a sum less than or equal to threshold or return 0 if there is no such square.

 

Example 1:


Input: mat = [[1,1,3,2,4,3,2],[1,1,3,2,4,3,2],[1,1,3,2,4,3,2]], threshold = 4
Output: 2
Explanation: The maximum side length of square with sum less than 4 is 2 as shown.
Example 2:

Input: mat = [[2,2,2,2,2],[2,2,2,2,2],[2,2,2,2,2],[2,2,2,2,2],[2,2,2,2,2]], threshold = 1
Output: 0
 

Constraints:

m == mat.length
n == mat[i].length
1 <= m, n <= 300
0 <= mat[i][j] <= 10^4
0 <= threshold <= 10^5

class Solution:

    def maxSideLength(self, mat: List[List[int]], threshold: int) -> int:
        s, m, n = 1, len(mat), len(mat[0])
        pref = [[0] * (n+1) for _ in range(m+1)]
        for i, j in product(range(m), range(n)):
            pref[i+1][j+1] = pref[i+1][j] + pref[i][j+1] - pref[i][j] + mat[i][j]
        for i, j in product(range(m), range(n)):
            while (i + s <= m and j + s <= n and 
                   pref[i+s][j+s] - pref[i+s][j] - pref[i][j+s] + pref[i][j] <= threshold):
                s += 1
        return s - 1 
