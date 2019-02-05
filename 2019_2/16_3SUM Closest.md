## 3sum closest

### description

Given an array nums of n integers and an integer target, find three integers in nums such that the sum is closest to target. Return the sum of the three integers. You may assume that each input would have exactly one solution.

Example:

Given array nums = [-1, 2, 1, -4], and target = 1.

The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

### vesion1. beat 77%

这题的思路跟3SUM一样，先选出一个数，然后通过left, right两个指针，选出sum最接近target的值，用一个额外的变量min_minus来记录3SUM-target的绝对值，选出最小答案

leetcode有点问题呀...同样的代码提交了两次一次beat20,一次beat77,那我就当它是77吧～

```java
class Solution {
    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);
        int result = 0;
        int min_minus = Integer.MAX_VALUE;
        int minus, sum;
        for (int i = 0; i < nums.length-2; i++) {
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                sum = nums[i] + nums[left] + nums[right];
                minus = sum - target;
                if (minus < 0) {
                    left++;
                } else if (minus > 0) {
                    right--;
                } else {
                    return target;
                }
                if (Math.abs(minus) < Math.abs(min_minus)) {
                    result = sum;
                    min_minus = minus;
                }
            }
        }
        return result;
    }
}
```