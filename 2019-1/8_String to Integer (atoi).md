## 8. String to Integer (atoi)

### description

Implement atoi which converts a string to an integer.

The function first discards as many whitespace characters as necessary until the first non-whitespace character is found. Then, starting from this character, takes an optional initial plus or minus sign followed by as many numerical digits as possible, and interprets them as a numerical value.

The string can contain additional characters after those that form the integral number, which are ignored and have no effect on the behavior of this function.

If the first sequence of non-whitespace characters in str is not a valid integral number, or if no such sequence exists because either str is empty or it contains only whitespace characters, no conversion is performed.

If no valid conversion could be performed, a zero value is returned.

Note:

Only the space character ' ' is considered as whitespace character.
Assume we are dealing with an environment which could only store integers within the 32-bit signed integer range: [−231,  231 − 1]. If the numerical value is out of the range of representable values, INT_MAX (231 − 1) or INT_MIN (−231) is returned.
Example 1:

Input: "42"
Output: 42
Example 2:

Input: "   -42"
Output: -42
Explanation: The first non-whitespace character is '-', which is the minus sign.
             Then take as many numerical digits as possible, which gets 42.
Example 3:

Input: "4193 with words"
Output: 4193
Explanation: Conversion stops at digit '3' as the next character is not a numerical digit.
Example 4:

Input: "words and 987"
Output: 0
Explanation: The first non-whitespace character is 'w', which is not a numerical 
             digit or a +/- sign. Therefore no valid conversion could be performed.
Example 5:

Input: "-91283472332"
Output: -2147483648
Explanation: The number "-91283472332" is out of the range of a 32-bit signed integer.
             Thefore INT_MIN (−231) is returned.


### version1. beat 87%

这题目本身没有什么难度，就是corner case比较多，需要注意。我的代码是根据错误提示，不断修改去兼容corner case,所以比较丑， 今天时间比较紧急，就不改善了= =。

```java
class Solution {
    public int myAtoi(String str) {
      if (str.length() == 0) return 0;
      long res = 0;
      char[] chars = str.toCharArray();
      boolean getFirst = false;
      boolean isPlus = true;
      int num;
      for (char c : chars) {
        if (' ' == c && getFirst) break;
        if (' ' == c && !getFirst) continue;
        if (getFirst) {
          num = c - '0';
          if (0 > num || num > 9) {
            break;
          } else {
            res = res*10 + num;
            if (res > Integer.MAX_VALUE) break;
          }
        } else {
          if ('-' == c) {
            isPlus = false;
            getFirst = true;
          } else if ('+' == c) {
            getFirst = true;
          } else {
            num = c - '0';
            if (0 > num || num > 9) break;
            getFirst = true;
            res = num;
          }
        }
      }
      res = isPlus ? res : 0-res;
      res = res > Integer.MAX_VALUE ? Integer.MAX_VALUE : res;
      res = res < Integer.MIN_VALUE ? Integer.MIN_VALUE : res;
      return (int) res;
    }
}

```