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
