## ZigZag Conversion

### version1. beat 58%

```java
class Solution {
    public String convert(String s, int numRows) {
        if (numRows == 1) return s;
        List<StringBuilder> res = new ArrayList<>();
        
        for (int i = 0; i < Math.min(s.length(), numRows); i++) {
            res.add(new StringBuilder());
        }
        
        int curRow = 0;
        int step = -1;
        for (char c : s.toCharArray()) {
            res.get(curRow).append(c);
            if (curRow == 0 || curRow == numRows-1) step = 0 - step;
            curRow += step;
        }
        StringBuilder sb = new StringBuilder();
        for (StringBuilder m: res) sb.append(m);
        return sb.toString();
    }
}
```

### Better solution

这题感觉没什么意义，更好的方法是直接计算出结果字符串每一个index与原来字符串的index的映射关系，我是看不出来..