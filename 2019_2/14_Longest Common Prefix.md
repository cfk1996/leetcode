## 14. Longest Common Prefix

### description

Write a function to find the longest common prefix string amongst an array of strings.

If there is no common prefix, return an empty string "".

Example 1:

Input: ["flower","flow","flight"]
Output: "fl"

Example 2:

Input: ["dog","racecar","car"]
Output: ""
Explanation: There is no common prefix among the input strings.

### version1 beat 79.40%

暴力遍历

```java
class Solution {
    public String longestCommonPrefix(String[] strs) {
        if (strs.length == 0) return "";
        StringBuilder sb = new StringBuilder("");
        char temp;
        int index = 0;
        boolean isDiff = false;
        while (index < strs[0].length()) {
            temp = strs[0].charAt(index);
            for (String s : strs) {
                if (index == s.length() || temp != s.charAt(index)) {
                    isDiff = true;
                    break;
                }
            }
            if (isDiff) {
                break;
            }
            sb.append(temp);
            index += 1;
        }
        return sb.toString();
    }
}
```

###

最近回老家过年了，虽然谈不上忙，但是老家这环境确实不适合上网啊。

实习结束离职了，没有了mac pro。现在的操作各种不爽，由奢入简难呀。

条件艰苦，刷题还是得继续，新年加油～