今日题目

给出一个区间的集合，请合并所有重叠区间。

示例 1:
输入: [[1,3],[2,6],[8,10],[15,18]]
输出: [[1,6],[8,10],[15,18]]
解释: 区间 [1,3] 和 [2,6] 重叠, 将它们合并为 [1,6].
示例 2:
输入: [[1,4],[4,5]]
输出: [[1,5]]
解释: 区间 [1,4] 和 [4,5] 可被视为重叠区间。


题目分析

先将目标区间数组从小到大排序，然后从第一个区间开始，如果相邻的两个区间，end小于start则合并区间，且生成新的区间，如果不小于，则放到返回区间，可以看下面几个例子。

[1,3][2,6] ->[1,6]

第一个区间的end大于等于第二个区间的start,同时第二个区间的end大于第一个区间的end。

[2,8][3,5] ->[2,8] 

第一个区间的end大于等于第二个区间的start,同时第二个区间的end小于第一个区间的end。

[1,2][3,4] -> [1,2][3,4]

第一个区间的end小于第二个区间的start 。


代码实现

# Definition for an interval.
# class Interval:
#     def __init__(self, s=0, e=0):
#         self.start = s
#         self.end = e

class Solution:
    def merge(self, intervals):
        """
        :type intervals: List[Interval]
        :rtype: List[Interval]
        """
        intervals.sort(key = lambda interval_tmp: interval_tmp.start)  
        N = len(intervals)
        s = []
        for i in range(N):
            flag = 0
            for j in range(len(s)):
                if not (intervals[i].start > s[j].end or intervals[i].end < s[j].start):
                    s[j].start = min(intervals[i].start, s[j].start)
                    s[j].end = max(intervals[i].end, s[j].end)
                    flag = 1
                    break
            if flag == 0:
                s.append(intervals[i])
        return s


