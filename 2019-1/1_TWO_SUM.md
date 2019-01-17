## TWO SUM

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution, and you may not use the same element twice.

Example:

Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].

### Version1

```java
import java.util.Arrays;
class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] s = Arrays.copyOf(nums,nums.length);
        Arrays.sort(nums);
        int left = 0;
        int right = nums.length-1;
        int sum;
        int[] numbers = new int[2];
        int[] result = new int[2];
        while (left < right) {
            sum = nums[left] + nums[right];
            if (sum == target) {
                numbers[0] = nums[left];
                numbers[1] = nums[right];
                break;
            } else if (sum > target) {
                right -= 1;
            } else {
                left += 1;
            }
        }
        int index = 0;
        for (int i = 0; i < s.length; i++) {
            if (s[i] == numbers[0] || s[i] == numbers[1]) {
                result[index] = i;
                index += 1;
                if (index==2) break;
            }
        }
        return result;
    }
}
```

### Version2

a better solution use HashMap in two pass.

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        map.put(nums[i], i);
    }
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement) && map.get(complement) != i) {
            return new int[] { i, map.get(complement) };
        }
    }
    throw new IllegalArgumentException("No two sum solution");
}
```

### Version3

more better solution with hashMap in ons pass.

```java
public int[] twoSum(int[] nums, int target) {
    Map<Integer, Integer> map = new HashMap<>();
    for (int i = 0; i < nums.length; i++) {
        int complement = target - nums[i];
        if (map.containsKey(complement)) {
            return new int[] { map.get(complement), i };
        }
        map.put(nums[i], i);
    }
    throw new IllegalArgumentException("No two sum solution");
}
```