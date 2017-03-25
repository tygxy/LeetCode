### 35.SearchInsertPosition
```java
	public class Solution {
	    public int searchInsert(int[] nums, int target) {
	        int i;
	        for(i=0;i < nums.length;i++){
	            if(nums[i] == target){
	                return i;
	            }else if(nums[i] > target){
	                return i;
	            }
	        }
	        return i;
	    }
	}
```

###  118.Pascal Triangle 1
```java
public class Solution {
    public List<List<Integer>> generate(int numRows) {
        List<List<Integer>> list = new ArrayList<>();
        if (numRows == 0){
            return list;
        }else{
            for (int i=0; i < numRows; i++){
                List<Integer> row = new ArrayList<Integer>();
                if (i == 0){
                    row.add(0, 1);
                }else{
                    List<Integer> prev = list.get(i - 1);
                    for (int j =0 ; j < i + 1; j++){
                        if (j == 0 || j == i){
                            row.add(j, 1);
                        }else {
                            row.add(j, prev.get(j - 1) + prev.get(j));
                        }
                    }
                }
                list.add(row);
            }
            return list;
        }
    }
}
```

### 119.Pascal Triangle 2
```java
public class Solution {
    public List<Integer> getRow(int rowIndex) {
        List<Integer> list = new ArrayList<>(rowIndex + 1);
        for (int i=0; i < rowIndex + 1; i++){
            list.add(i, 1);
        }
        if (rowIndex == 0 || rowIndex == 1){
            return list;
        }
        for (int j=2; j < rowIndex + 1; j++){
            int tmp, prev = list.get(0);
            for (int k = 1; k < j; k++){
                tmp = list.get(k);
                list.set(k, list.get(k) + prev);
                prev = tmp;
            }
        }
        return list;
    }
}
```

### 121.Best Time to Buy and Sell Stock
```java
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0){
            return 0;
        }
        int maxProfit = 0;
        int sofarMin = prices[0];
        for (int i = 0; i < prices.length; i++){
            if( prices[i] > sofarMin){
                maxProfit = Math.max(maxProfit, prices[i] - sofarMin);
            }else{
                sofarMin = prices[i];
            }
        }
        return maxProfit;
    }
    
}
```

### 66.Plus One
```java
public class Solution {
    public int[] plusOne(int[] digits) {
        boolean flag = false;
        for (int i = digits.length - 1; i >= 0; i--){
            int newnum = digits[i] + 1;
            if (newnum > 9){
                digits[i] = 0;
                if (i == 0){
                    flag = true;
                }
            }else{
                digits[i] = newnum;
                break;
            }
        }
        if (flag == false){
            return digits;
        }else {
            int [] newdigits = new int[digits.length + 1];
            newdigits[0] = 1;
            for (int k = 1; k < digits.length; k++){
                newdigits[k + 1] = digits[k];
            }
            return newdigits;
        }
    }
}
```

### 26.Remove Duplicates from Sorted Array
```java
public class Solution {
    public int removeDuplicates(int[] nums) {
        if (nums.length == 0){
            return 0;
        }
        int j = 0;
        for (int i = 0; i < nums.length; i++){
            if (nums[i] != nums[j]){
                j++;
                nums[j] = nums[i];
            }
        }
        return ++j;
    }
}
```

### 1.Two Sum
```java
public class Solution {
    public int[] twoSum(int[] nums, int target) {
        int[] result = new int[2];
        for (int i = 0; i < nums.length - 1; i++){
            for (int j = i + 1; j < nums.length; j++){
                if (nums[i] + nums[j] == target){
                    result[0] = i;
                    result[1] = j;
                }
            }
        }
        return result;
    }
}
```

### 27.Remove Element
```java
public class Solution {
    public int removeElement(int[] nums, int val) {
        if (nums.length == 0){
            return 0;
        }
        int j = 0;
        for(int i = 0; i < nums.length; i++){
            if (nums[i] != val){
                nums[j] = nums[i];
                j++;
            }
        }
        return j++;
    }
}
```
### 122.Best Time to Buy and Sell Stock II
```
public class Solution {
    public int maxProfit(int[] prices) {
        if (prices.length == 0){
            return 0;
        }
        int maxProfit = 0;
        int i = 0;
        while(i != prices.length - 1){
            if( prices[i] < prices[i + 1]){
                maxProfit += prices[i + 1] - prices[i];
            }
            i++;
        }
        return maxProfit;
    }
}
```

### 268.Missing Number
- My Solution 
```java
public class Solution {
    public int missingNumber(int[] nums) {
       if(nums.length == 0){
           return 0;
       }else{
           int i;
           for (i = 0; i < nums.length; i++){
               for (int j = i; j < nums.length; j++){
                   if (nums[j] == i){
                       if (j == i){
                           break;
                       }else{
                           int tmp = nums[i];
                           nums[i] = nums[j];
                           nums[j] = tmp;
                           break;
                       }
                   }
                   if (j == nums.length - 1){
                       return i;
                   }
               }
           }
           return i;
       }
    }
}
```
- Better Solution
```
public class Solution {
    public int missingNumber(int[] nums) {
       int sum = 0;
       for (int i : nums){
           sum += i;
       }
       return (nums.length * (nums.length + 1)) / 2 - sum;
    }
}
```

### 217. Contains Duplicate
```
public class Solution {
    public boolean containsDuplicate(int[] nums) {
        if(nums.length == 0){
            return false;
        }else{
            Map m = new HashMap();
            for(int val : nums){
                m.put(val,1);
            }
            if(m.size() < nums.length){
                return true;
            }else{
                return false;
            }
        }
    }
}
```

### 169. Majority Element
- My Solution
```java
public class Solution {
    public int majorityElement(int[] nums) {
        int result = 0;
        Map<Integer, Integer> m = new HashMap<Integer, Integer>();
        for (int val : nums) {
            if (m.containsKey(val)) {
                m.put(val,m.get(val) + 1);
            }else {
                m.put(val, 1);
            }
            if (m.get(val) > nums.length / 2) {
                result = val;
                break;
            }
        }
        return result;
    }
}
```
- better Solution
```java
public class Solution {
    public int majorityElement3(int[] nums) {
        int count=0, ret = 0;
        for (int num: nums) {
            if (count==0)
                ret = num;
            if (num!=ret)
                count--;
            else
                count++;
        }
        return ret;
    }
}

```
### 167. Two Sum II - Input array is sorted
```java
public class Solution {
    public int[] twoSum(int[] numbers, int target) {
        if (numbers.length < 2) {
            return null;
        }else {
            int[] result = new int[2];
            int l = 0;
            int r = numbers.length - 1;
            while (l < r) {
                int sum = numbers[l] + numbers[r];
                if (sum == target) {
                    result[0] = l + 1;
                    result[1] = r + 1;
                    break;
                }else if (sum < target) {
                    l++;
                }else {
                    r--;
                }
            }
            return result;
        }
    }
}
```
### 88. Merge Sorted Array
- My Solution
```java
public class Solution {
    public void merge(int[] nums1, int m, int[] nums2, int n) {
        if (m == 0){
            for (int i = 0; i < n; i++) {
                nums1[i] = nums2[i];
            }
        }else{
            if (n != 0) {
                int i = m - 1;
                int j = n - 1;
                int k = m + n - 1;
                while(k >= 0) {
                    if (nums1[i] >= nums2[j]) {
                        nums1[k--] = nums1[i--];
                        if (i < 0) {
                            while (k >= 0) {
                                nums1[k--] = nums2[j--];
                            }
                            break;
                        }
                    }else {
                        nums1[k--] = nums2[j--];
                        if (j < 0) {
                            break;
                        }
                    }
                }
            }
        }
    }
}
```
- Better Solution
```java
class Solution {
    public void merge(int A[], int m, int B[], int n) {
        int i=m-1;
        int j=n-1;
        int k = m+n-1;
        while(i >=0 && j>=0)
        {
            if(A[i] > B[j])
                A[k--] = A[i--];
            else
                A[k--] = B[j--];
        }
        while(j>=0)
            A[k--] = B[j--];
    }
}
```

### 53. Maximum Subarray
```java
public class Solution {
    public int maxSubArray(int[] nums) {
        int max = Integer.MIN_VALUE;
        int sum = 0;
        for (int i = 0; i < nums.length; i++) {
            sum += nums[i];
            max = Math.max(sum, max);
            sum = Math.max(sum, 0);
        }
        return max;
    }
}
```
