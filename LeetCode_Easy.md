# LeetCode(Easy)

## 1.汇总
- 未能独立解决 500,292,448,104,371,226
- 独立解决，需要改进 496,136,520,521,258,283,492
- 完全独立解决 561,461,566,557,476,412,344,463,485,575

## 2.规律
- 找一个不同的题，考虑xor
    - 0 ^ A = A; A ^ A = 0
- 树的问题，很多都是靠栈来解决

## 3.题目

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
### 448. Find All Numbers Disappeared in an Array
```java
public class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> list = new ArrayList<>();
        for (int i = 0; i < nums.length; i++) {
            if (nums[Math.abs(nums[i]) - 1] > 0) {
                nums[Math.abs(nums[i]) - 1] = -nums[Math.abs(nums[i]) - 1];
            }
        }
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] > 0) {
                list.add(i + 1);
            }
        }
        return list;
    }
}
```

### 521. Longest Uncommon Subsequence I
```java
public class Solution {
    public int findLUSlength(String a, String b) {
        if (a.length() != b.length()) {
            return Math.max(a.length(), b.length());
        }else {
            return a.contains(b) ? -1 : a.length();
        }
    }
}
```

### 104. Maximum Depth of Binary Tree
```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public int maxDepth(TreeNode root) {
        if (root == null) {
            return 0;
        }
        int maxDepth = 0;
        Stack<TreeNode> stack = new Stack<>();
        Stack<Integer> sub = new Stack<>();
        stack.push(root);
        sub.push(1);
        while (!stack.isEmpty()) {
            TreeNode p = stack.pop();
            int tempVal = sub.pop();
            if (p.left == null && p.right == null) {
                maxDepth = Math.max(maxDepth, tempVal);
            }else {
                if (p.left != null) {
                    stack.push(p.left);
                    sub.push(tempVal + 1);
                }
                if (p.right != null) {
                    stack.push(p.right);
                    sub.push(tempVal + 1);
                }
            }
        }
        return maxDepth;
    }
}
```
### 389. Find the Difference
- solution
```java
public class Solution {
    public char findTheDifference(String s, String t) {
        List<Character> listS = new ArrayList<>();
        List<Character> listT = new ArrayList<>();
        for (int i = 0; i < s.length(); i++) {
            listS.add(s.charAt(i));
        }
        for (int i = 0; i < t.length(); i++) {
            listT.add(t.charAt(i));
        }
        Collections.sort(listS);
        Collections.sort(listT);
        for (int i = 0; i < listT.size() - 1; i++) {
            if (listS.get(i) != listT.get(i)) {
                return listT.get(i);
            }
        }
        return listT.get(listT.size() - 1);
    }
}
```
- better solution
```
public char findTheDifference(String s, String t) {
    char c = 0;
    for (int i = 0; i < s.length(); ++i) {
        c ^= s.charAt(i);
    }
    for (int i = 0; i < t.length(); ++i) {
        c ^= t.charAt(i);
    }
    return c;
}
```

### 371. Sum of Two Integers
```java
// 简而言之就是用异或算不带进位的和，用与并左移1位来算进位，然后把两者加起来即可
public class Solution {
    public int getSum(int a, int b) {
        if (a == 0) return b;
        if (b == 0) return a;
        while (b != 0) {
            int carry = a & b;
            a = a ^ b;
            b = carry << 1;
        }
        return a;
    }
}
```
### 258. Add Digits
- solution
```java
public class Solution {
    public int addDigits(int num) {
        String result = String.valueOf(num);
        while (result.length() > 1) {
            int sum = 0;
            for (int i = 0; i < result.length(); i++) {
                sum += Integer.parseInt(String.valueOf(result.charAt(i)));
            }
            result = String.valueOf(sum);
        }
        return Integer.parseInt(result);
    }
}
```
- better solution
```java
public class Solution {
    public int addDigits(int num) {
        if (num == 0){
            return 0;
        }
        if (num % 9 == 0){
            return 9;
        }
        else {
            return num % 9;
        }
    }
}
```
### 283. Move Zeroes
- solution
```java
public class Solution {
    public void moveZeroes(int[] nums) {
         for (int i = 0; i < nums.length - 1; i++) {
            if (nums[i] == 0) {
                int j = i + 1;
                while (j < nums.length) {
                    if (nums[j] != 0) {
                        break;
                    }
                    if (j == nums.length - 1) {
                        break;
                    }
                    j++;
                }
                nums[i] = nums[j];
                nums[j] = 0;
            }
        }
    }
}
```
- better solution
```java
public void moveZeroes(int[] nums) {
    if (nums == null || nums.length == 0) return;        

    int insertPos = 0;
    for (int num: nums) {
        if (num != 0) nums[insertPos++] = num;
    }        

    while (insertPos < nums.length) {
        nums[insertPos++] = 0;
    }
}
```
### 575. Distribute Candies
```java
public class Solution {
    public int distributeCandies(int[] candies) {
        Set<Integer> set = new HashSet<Integer>();
        for (int c : candies) {
            set.add(c);
        }
        if (set.size() < candies.length / 2) {
            return set.size();
        }else {
            return candies.length / 2;
        }
    }
}
```
### 226. Invert Binary Tree
```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) {
            return null;
        }
        TreeNode tmpRight = root.right;
        root.right = invertTree(root.left);
        root.left = invertTree(tmpRight);
        return root;
    }
}
```
```java
public class Solution {
    public TreeNode invertTree(TreeNode root) {
        if(root == null) {
            return null;
        }
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while(!stack.isEmpty()) {
            TreeNode node = stack.pop();
            TreeNode left = node.left;
            node.left = node.right;
            node.right = left;
            
            if (node.right != null) {
                stack.push(node.right);
            }
            if (node.left != null) {
                stack.push(node.left);
            }
        }
        return root;
    }
}
```
### 492. Construct the Rectangle
- mysolution
```java
public class Solution {
    public int[] constructRectangle(int area) {
        int[] result = {area,1};
        int tmpWight;
        int tmpLength;
        for (int i = area; i >= 1; i--) {
            if (area % i == 0) {
                tmpLength = i;
                tmpWight = area / i;
                if (Math.abs(tmpLength - tmpWight) < Math.abs(result[0] - result[1]) ) {
                    result[0] = tmpLength;
                    result[1] = tmpWight;
                }
                if (tmpLength < tmpWight) {
                    return result;
                }
            }
        }
        return result;
    }
}
``` 
- better solution
```java
public int[] constructRectangle(int area) {
    int[] result = new int[2];
    if(area == 0){
        return result;
    }
    int a = (int)Math.sqrt(area);
    while(area%a != 0){
        a--;
    }
    int b = area/a;
    result[0] = b;
    result[1] = a;
    return result;
}
```