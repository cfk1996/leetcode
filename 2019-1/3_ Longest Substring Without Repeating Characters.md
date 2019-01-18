##  Longest Substring Without Repeating Characters

Given a string, find the length of the longest substring without repeating characters.

Example 1:
Input: "abcabcbb"
Output: 3 
Explanation: The answer is "abc", with the length of 3.

Example 2:
Input: "bbbbb"
Output: 1
Explanation: The answer is "b", with the length of 1.

Example 3:
Input: "pwwkew"
Output: 3
Explanation: 
The answer is "wke", with the length of 3. 
Note that the answer must be a substring, "pwke" is a subsequence and not a substring.

### Version1.beat42%

```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int max = 0, index;
        int front = 0;
        Map<Character, Integer> count = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            if (count.containsKey(s.charAt(i))) {
                // remove char before s[i]
                index = count.get(s.charAt(i));
                for (int j = front; j <= index; j++) {
                    count.remove(s.charAt(j));
                }
                front = index+1;
            } 
            count.put(s.charAt(i),i);
            if (count.size() > max) {
                max = count.size();
            }
        }
        return max;
    }
}
```

### Version2.beat67%
```java
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int max = 0, index = 0;
        int temp_res = 0;
        Map<Character, Integer> count = new HashMap<>();
        for (int i = 0; i < s.length(); i++) {
            if (count.containsKey(s.charAt(i))) {
                index = Math.max(count.get(s.charAt(i)), index);
                temp_res = i - index;
            } else {
                temp_res += 1;
            }
            max = Math.max(max, temp_res);
            count.put(s.charAt(i),i);
        }
        return max;
    }
}
```

version2比version1好的原因在于，滑动窗口的判断上，version1通过HashMap维护当前的字符串，version2靠index下标来标记滑动窗口的起动位置。

另外看了下一些最优解，其实算法的思路都是差不多的，都是通过滑动窗口来遍历一遍字符串。但是因为这是字符串，且字符的可能情况在char字符的0～128的范围内，所以用数组代替map

### Version3.beat96%

```java
public class Solution {
    public int lengthOfLongestSubstring(String s) {
        int n = s.length(), ans = 0;
        int[] index = new int[128]; // current index of character
        // try to extend the range [i, j]
        for (int j = 0, i = 0; j < n; j++) {
            i = Math.max(index[s.charAt(j)], i);
            ans = Math.max(ans, j - i + 1);
            index[s.charAt(j)] = j + 1;
        }
        return ans;
    }
}
```