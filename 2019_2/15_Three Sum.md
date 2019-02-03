## 3Sum

### description

Given an array nums of n integers, are there elements a, b, c in nums such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note:

The solution set must not contain duplicate triplets.

Example:

Given array nums = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]


### version1 beat 51%

暴力遍历，跳过重复的

```java
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        if (nums.length == 0) return result;
        Arrays.sort(nums);
        for (int i = 0; i < nums.length-2; i++) {
            if (i > 0 && nums[i] == nums[i-1]) {
                continue;
            }
            int left = i + 1;
            int right = nums.length - 1;
            while (left < right) {
                if (left > i+1 && nums[left] == nums[left-1]) {
                    left += 1;
                    continue;
                }
                if (right < nums.length - 1 && nums[right] == nums[right+1]) {
                    right -= 1;
                    continue;
                }
                if (nums[left]+nums[right] == 0 - nums[i]) {
                    result.add(new ArrayList<>(Arrays.asList(nums[i],nums[left],nums[right])));
                    left++;
                    right--;
                } else if (nums[left]+nums[right] < 0 - nums[i]) {
                    left ++;
                } else {
                    right --;
                }
            }
        }
        return result;
    }
}
```