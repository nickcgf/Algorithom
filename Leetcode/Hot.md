

# 重点题

##  [最长公共子序列](https://leetcode.cn/problems/longest-common-subsequence/description/)



##  [编辑距离](https://leetcode.cn/problems/edit-distance/description/)



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

