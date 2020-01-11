## Increasing Triplet Subsequence

Given an unsorted array return whether an increasing subsequence of length 3 exists or not in the array.

Formally the function should:

Return true if there exists i, j, k
such that arr[i] < arr[j] < arr[k] given 0 ≤ i < j < k ≤ n-1 else return false.
Note: Your algorithm should run in O(n) time complexity and O(1) space complexity.

Example 1:

Input: [1,2,3,4,5]
Output: true
Example 2:

Input: [5,4,3,2,1]
Output: false
在真实的面试中遇到过这道题？

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/increasing-triplet-subsequence


### Version1

这道题需要在无序的序列中找到三个递增的数，大概思路就是
1. 先找到第一个数记为a（序列的第一个数）
2. 找到第一个数后，继续遍历，如果当前数值大于第一个数，则是一个合适的数，记为b；如果小于第一个数，则替换第一个数a的值；如果等于a，跳过
3. 找到第二个数后，继续遍历，如果当前值大于b，则说明已经找到递增的三个数，返回true.如果小于a，则更新a，小于b则更新b。
4. 遍历结束后还没有返回说明不存在这种序列，return false。

这里的关键是在遍历时即使找到比a小的数，更新了a的值，也不会影响之前已经找到的结果。如[2,3,1,4]这个序列

1. 找到a=2,
2. 因为3>2,找到b=3，这是已经可以得出有长度为2的递增序列【2，3】了，只要再找一个大于3的值，就能满足存在长度为3的递增序列
3. 遍历的第三个值为1，小于a,所以更新a=1，但是这并没有改变已经找到【2，3】这个长度为2的递增序列的事实。
4. 遍历第四个值4>b，所以找到了长度为3的序列

再如[2,3,1,2,4]这个序列
前三步与上面一样，得到a=1,b=3
4. 遍历第四个值2，因为2 > a,且2 < b,所以更新b=2（显然[1,2]比[2,3]更容易找到一个递增序列）

```java
class Solution {
    public boolean increasingTriplet(int[] nums) {
        int a = Integer.MAX_VALUE;
        int b = Integer.MAX_VALUE;
        for (int num : nums) {
            if (num < a) {
                a = num;
            } else if (a < num && num < b) {
                b = num;
            } else if (num > b) {
                return true;
            }
        }
        return false;
    }
}
```