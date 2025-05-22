


# 滑动窗口


## 基本套路
1. 进入窗口（没满足某个条件就继续更新）
2. 更新答案
3. 退出窗口

## [定长子串中元音的最大数目](https://leetcode.cn/problems/maximum-number-of-vowels-in-a-substring-of-given-length/)
```
class Solution:
    def maxVowels(self, s: str, k: int) -> int:
        vowels = set("aeiou")
        ans = 0
        
        l, r = 0, 0 
        temp = 0
        while r < len(s):
            # 入
            if s[r] in vowels:
                temp += 1
                ans = max(temp, ans) # 更新
            if r < k - 1: 
                r += 1
                continue
            r += 1
            # 出
            if s[l] in vowels:
                temp -= 1
            l += 1
        return ans
```


