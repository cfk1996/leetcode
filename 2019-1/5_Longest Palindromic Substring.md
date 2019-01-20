## Longest Palindromic Substring

Given a string s, find the longest palindromic substring in s. You may assume that the maximum length of s is 1000.

Example 1:

Input: "babad"
Output: "bab"
Note: "aba" is also a valid answer.
Example 2:

Input: "cbbd"
Output: "bb"

Version1. beat 50%

```java
class Solution {
  public String longestPalindrome(String s) {
    if (s.length() == 0) {
      return "";
    }
    char[] c = s.toCharArray();
    String max = "";
    int count = 0;
    int left = 0;
    int right = 0;
    for (int i = 0; i < c.length; i++) {
      //even
      for (int j = 0; i-j >= 0 && i+j+1 < c.length; j++) {
        if (c[i-j] != c[i+j+1]) {
          break;
        }
        count = j * 2 + 2;
        left = i - j;
        right = i + j + 1;
      }
      if (count > max.length()) {
        max = s.substring(left, right + 1);
      }
      // odd
      for (int j = 0; i-j >= 0 && i+j < c.length; j++) {
        if (c[i-j] != c[i+j]) {
          break;
        }
        count = j * 2 + 1;
        left = i - j;
        right = i + j;
      }
      if (count > max.length()) {
        max = s.substring(left, right + 1);
      }
    }
    return max;
  }
}
```

Version2.

[Manacher 算法](https://segmentfault.com/a/1190000003914228)