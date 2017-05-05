# LeetCode(Easy)

## 1.汇总
- 未能独立解决 500,292,
- 独立解决，需要改进 496,136,520
- 完全独立解决 561,461,566,557,476,412,344,463,485

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

### 412. Fizz Buzz
```
public class Solution {
    public List<String> fizzBuzz(int n) {
        List<String> list = new ArrayList<>();
        for (int i = 1; i <= n; i++) {
            if ((i % 3 == 0) && (i % 5 == 0)) {
                list.add("FizzBuzz");
            }else if (i % 3 == 0) {
                list.add("Fizz");
            }else if (i % 5 == 0) {
                list.add("Buzz");
            }else {
                list.add(String.valueOf(i));
            }
        }
        return list;
    }
}
```

### 344. Reverse String
```java
public class Solution {
    public String reverseString(String s) {
        StringBuffer sb = new StringBuffer(s);
        return sb.reverse().toString();
    }
}
```

### 496. Next Greater Element I
- solution
```
public class Solution {
    public int[] nextGreaterElement(int[] findNums, int[] nums) {
        Map<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < nums.length; i++) {
            boolean flag = false;
            for (int j = i; j < nums.length; j++) {
                if (nums[i] < nums[j]) {
                    map.put(nums[i], nums[j]);
                    flag = true;
                    break;
                }
            }
            if (flag == false) {
                map.put(nums[i], -1);
            }
        }
        int[] result = new int[findNums.length];
        for (int i = 0; i < findNums.length; i++) {
            result[i] = map.get(findNums[i]);
        }
        return result;
    }
}
```
- better solution
```java
public int[] nextGreaterElement(int[] findNums, int[] nums) {
    Map<Integer, Integer> map = new HashMap<>(); // map from x to next greater element of x
    Stack<Integer> stack = new Stack<>();
    for (int num : nums) {
        while (!stack.isEmpty() && stack.peek() < num)
            map.put(stack.pop(), num);
        stack.push(num);
    }   
    for (int i = 0; i < findNums.length; i++)
        findNums[i] = map.getOrDefault(findNums[i], -1);
    return findNums;
}
```

### 463. Island Perimeter
```java
public class Solution {
    public int islandPerimeter(int[][] grid) {
        int perimeter = 0;
        if (grid != null) {
            int row = grid.length;
            int col = grid[0].length;
            for (int i = 0; i < row; i++) {
                for (int j = 0; j < col; j++) {
                    if(grid[i][j] == 1) {
                        perimeter += 4;
                        if (j != col - 1) {
                            if (grid[i][j + 1] == 1) {
                                perimeter -= 2;
                            }
                        }
                        if (i != row - 1) {
                            if (grid[i + 1][j] == 1) {
                                perimeter -= 2;
                            }
                        }
                    }
                }
            }
        }
        return perimeter;
    }
}
```

### 292. Nim Game
```java
public class Solution {
    public boolean canWinNim(int n) {
        if (n % 4 != 0) {
            return true;
        }else {
            return false;
        }
    }
}
```

### 485. Max Consecutive Ones
```java
public class Solution {
    public int findMaxConsecutiveOnes(int[] nums) {
        int max = 0;
        int tmp = 0;
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] == 0) {
                tmp = 0;
            }else {
                tmp += 1;
            }
            if (tmp > max) {
                max = tmp;
            }
        }
        return max;
    }
}
```

### 136. Single Number
- solution
```
public class Solution {
    public int singleNumber(int[] nums) {
        Set<Integer> set = new HashSet<>();
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            set.add(nums[i]);
            sum += nums[i];
        }
        Iterator<Integer> it = set.iterator();
        while (it.hasNext()) {
            sum -= (2 * (Integer)it.next());
        }
        return -sum;
    }
}
```
- better solution
```java
public class Solution {
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int i = 0; i < nums.length; i++) {
            result ^= nums[i];
        }
        return result;
    }
}
```

### 520. Detect Capital
- solution
```
public class Solution {
    public boolean detectCapitalUse(String word) {
        if (word != null) {
            if (word.toLowerCase() == word) {
                return true;
            }else if (word.toUpperCase() == word) {
                return true;
            }else {
                char[] arr = word.toCharArray();
                for (int i = 0; i < arr.length; i++) {
                    if (arr[i] >= 'A' && arr[i] <= 'Z' && i != 0) {
                        return false;
                    }
                }
                return true;
            }
        }else {
            return false;
        }
    }
}
```
- better solution
```
public class Solution {
    public boolean detectCapitalUse(String word) {
        int cnt = 0;
        for(char c: word.toCharArray()) if('Z' - c >= 0) cnt++;
        return ((cnt==0 || cnt==word.length()) || (cnt==1 && 'Z' - word.charAt(0)>=0));
    }
}

```


