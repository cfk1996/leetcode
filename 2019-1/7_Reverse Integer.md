## Reverse Integer

Given a 32-bit signed integer, reverse digits of an integer.

Example 1:

Input: 123
Output: 321
Example 2:

Input: -123
Output: -321
Example 3:

Input: 120
Output: 21
Note:
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. For the purpose of this problem, assume that your function returns 0 when the reversed integer overflows.

### version1. beat 84%

我第一次提交的代码不是这样的，这是参考了最优解的答案。我一开始把正负分开讨论，多用了个布尔变量来控制返回值的正负，后来发现负数一样可以取余...

```java
class Solution {
    public int reverse(int x) {
        long res = 0;
        int left;
        while (x != 0) {
            left = x % 10;
            x = x / 10;
            res = res*10 + left;
        }
        return res == (int) res ? (int) res : 0;
    }
}
```