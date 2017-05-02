# LeetCode(Easy)

## 1.汇总
- 未能独立解决
- 独立解决，需要改进
- 完全独立解决 561,461,566

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
