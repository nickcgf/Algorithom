

# 重点题

##  [最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/description/)
```
class Solution:
    def longestCommonSubsequence(self, text1: str, text2: str) -> int:
        m, n = len(text1), len(text2)
        dp = [[0] * (n+1) for _ in range(m+1)]
        for i in range(1,m+1):
            for j in range(1, n+1):
                if text1[i-1] == text2[j-1]:
                    dp[i][j] = dp[i-1][j-1] + 1
                else:
                    dp[i][j] = max(dp[i-1][j], dp[i][j-1])
        
        return dp[m][n]
```

##  [编辑距离](https://leetcode.cn/problems/edit-distance/description/)
```
class Solution:
    def minDistance(self, word1: str, word2: str) -> int:
        m, n = len(word1), len(word2)
        dp = [[0 for _ in range(n+1)] for _ in range(m+1)]

        for i in range(1,m+1):
            dp[i][0] = i
        for j in range(1,n+1):
            dp[0][j] = j

        for i in range(1, m+1):
            for j in range(1, n+1):
                if word1[i-1] == word2[j-1]:
                    dp[i][j] = dp[i-1][j-1]
                else:
                    dp[i][j] = min(dp[i-1][j], dp[i][j-1], dp[i-1][j-1]) + 1
            # print(dp[i])
        return dp[m][n]
```

## [寻找两个正序数组的中位数](https://leetcode.cn/problems/median-of-two-sorted-arrays/description/)
```
class Solution:
    def findMedianSortedArrays(self, nums1: List[int], nums2: List[int]) -> float:
        m, n = len(nums1), len(nums2)
        def getKthElement(k:int)->int:
            offset1, offset2 = 0, 0
            while True:
                if offset1 == m:
                    return nums2[offset2+k-1]
                if offset2 == n:
                    return nums1[offset1+k-1]
                if k == 1:
                    # print(offset1,offset2)
                    return min(nums1[offset1], nums2[offset2])
                
                temp = k // 2 - 1
                index1 = min(m-1, temp + offset1)
                index2 = min(n-1, temp + offset2)
                # print("idx:",index1,index2)
                if nums1[index1] <= nums2[index2]:
                    k -= index1 - offset1 + 1
                    offset1 = index1 + 1
                else:
                    k -= index2 - offset2 + 1
                    offset2 = index2 + 1
                # print(k, offset1, offset2)
        
        if (n+m) % 2 == 1:
            return getKthElement((n+m+1) // 2)
        return (getKthElement((n+m)//2) + getKthElement((n+m)//2 + 1))/2.0
```

