## 11.Container With Most Water

### description

Given n non-negative integers a1, a2, ..., an , where each represents a point at coordinate (i, ai). n vertical lines are drawn such that the two endpoints of line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis forms a container, such that the container contains the most water.

![示例](https://raw.githubusercontent.com/cfk1996/leetcode/master/pictures/img_9.jpg)

### version1. beat 86%

用left,right表示当前储水的长方形的左右边界，不断向内缩小范围，寻找最大解。

缩小的原则是，选择短的一侧进行向内收缩（木桶原理？）

```java
class Solution {
    public int maxArea(int[] height) {
        if (height.length < 2) return 0;
        int left = 0;
        int right = height.length - 1;
        int size = 0;
        int temp;
        while (left < right) {
            if (height[left] <= height[right]) {
                temp = (right - left) * height[left];
                if (temp > size) {
                    size = temp;
                } 
                left += 1;
            } else {
                temp = (right - left) * height[right];
                if (temp > size) {
                    size = temp;
                }
                right -= 1;
            }
        }
        return size;
    }
}
```


