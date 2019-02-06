## 17. Letter Combinations of a Phone Number

### description

Given a string containing digits from 2-9 inclusive, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below. Note that 1 does not map to any letters.

Example:

Input: "23"
Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

### version1. beat 82%

```java
class Solution {
    public List<String> letterCombinations(String digits) {
        Map<Character, String> maps = new HashMap<>();
        maps.put('2', "abc");
        maps.put('3', "def");
        maps.put('4', "ghi");
        maps.put('5', "jkl");
        maps.put('6', "mno");
        maps.put('7', "pqrs");
        maps.put('8', "tuv");
        maps.put('9', "wxyz");
        List<String> result = new ArrayList<>();
        List<String> append = new ArrayList<>();
        String temp;
        char[] chars = digits.toCharArray();
        for (char c : chars) {
            if (c == '1') {
                continue;
            } else if (maps.containsKey(c)) {
                temp = maps.get(c);
                if (result.size() == 0) {
                    for (char cs : temp.toCharArray()) {
                        append.add(String.valueOf(cs));
                    }
                } else {
                    for (char cs : temp.toCharArray()) {
                        for (String str : result) {
                            append.add(str + cs);
                        }
                    }
                }
            } else {
                // no need, all char in 1-9
                continue;
            }
            result = append;
            append = new ArrayList<>();
        }
        return result;
    }
}
```