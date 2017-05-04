# LeetCode(Easy)

## 1.汇总
- 未能独立解决 500
- 独立解决，需要改进
- 完全独立解决 561,461,566,476

## 2.题目

### 561. Array Partition I
```java
public class Solution {
    public int arrayPairSum(int[] nums) {
        Arrays.sort(nums);
        int sum = 0;
        for (int i = 0; i < nums.length; i += 2) {
            sum += nums[i];
        }
        return sum;
    }
}
```

### 461. Hamming Distance
```java
public class Solution {
    public int hammingDistance(int x, int y) {
        String binArr = Integer.toBinaryString(x ^ y);
        int hammingDistance = 0;
        for (int i = 0; i < binArr.length(); i++) {
            if (binArr.charAt(i) == '1') {
                hammingDistance += 1;
            }
        }
        return hammingDistance;
    }
}
```

### 566. Reshape the Matrix
```java
public class Solution {
    public int[][] matrixReshape(int[][] nums, int r, int c) {
        int oldR = nums.length;
        int oldC = nums[0].length;
        if (oldR * oldC != r * c) {
            return nums;
        }else {
            int [][] newMatrix = new int[r][c];
            int oldCount = 0;
            for (int i = 0; i < r; i++) {
                for (int j = 0; j < c; j++) {
                    newMatrix[i][j] = nums[oldCount / oldC][oldCount % oldC];
                    oldCount += 1;
                }
            }
            return newMatrix;
        }

    }
}
```

### 557. Reverse Words in a String III
```java
public class Solution {
    public String reverseWords(String s) {
        String[] arr = s.split("\\s+");
        StringBuffer sb = new StringBuffer();
        for (String str : arr) {
            StringBuffer temp = new StringBuffer(str);
            sb.append(temp.reverse());
            sb.append(" ");
        }
        sb.setLength(sb.length() - 1);
        return sb.toString();
    }
}
```

### 476. Number Complement
```java
public class Solution {
    public int findComplement(int num) {
        StringBuffer sb = new StringBuffer(Integer.toBinaryString(num));
        for (int i = 0; i < sb.length(); i++) {
            if (sb.charAt(i) == '1') {
                sb.setCharAt(i,'0');
            }else {
                sb.setCharAt(i,'1');
            }
        }
        return Integer.valueOf(sb.toString(),2);
    }
}
```

### 500. Keyboard Row
```java
public class Solution {
    public String[] findWords(String[] words) {
        String[] strs = {"QWERTYUIOP", "ASDFGHJKL", "ZXCVBNM"};
        Map<Character, Integer> map = new HashMap<>();
        for (int i = 0; i < strs.length; i++) {
            for (char c : strs[i].toCharArray()) {
                map.put(c, i);
            }
        }
        List<String> res = new ArrayList<>();
        for (String w : words) {
            if (w.equals("")) {
                continue;
            }
            int index = map.get(w.toUpperCase().charAt(0));
            for (char c : w.toUpperCase().toCharArray()) {
                if (map.get(c) != index) {
                    index = -1;
                    break;
                }
            }
            if (index != -1) {
                res.add(w);
            }
        }
        return res.toArray(new String[0]);
    }
}
```

