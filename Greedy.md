## [Easy] 455. Assign Cookies
**Link** : https://leetcode.com/problems/assign-cookies/description/
```
class Solution {
    public int findContentChildren(int[] g, int[] s) {
        Arrays.sort(g);
        Arrays.sort(s);

        int result = 0;
        int index = s.length - 1;
        for(int i = g.length - 1;i >= 0;i--){
            if(index >= 0 && s[index] >= g[i]){
                result++;
                index--;
            }
        }
        return result;
    }
} 
```
## [Medium] 376. Wiggle Subsequence
**Link** : https://leetcode.com/problems/wiggle-subsequence/description/
```
class Solution {
    public int wiggleMaxLength(int[] nums) {
        if(nums.length <= 1){
            return nums.length; 
        }

        int preDiff = 0;
        int count = 1;
        for(int i = 1;i < nums.length;i++){
            int curDiff = nums[i] - nums[i - 1];
            if((curDiff > 0 && preDiff <= 0) || (curDiff < 0 && preDiff >= 0)){
                count++;
                preDiff = curDiff;
            }
        }
        return count;
    }
}
```
## [Medium] 53. Maximum Subarray
**Link** : https://leetcode.com/problems/maximum-subarray/description/
```
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums.length == 1){
            return nums[0];
        }

        int result = Integer.MIN_VALUE;
        int count = 0;
        for(int i = 0;i < nums.length;i++){
            count += nums[i];
            result = Math.max(result,count);
            if(count < 0){
                count = 0;
            }
        }
        return result;
    }
}
```

## [Medium] 122. Best Time to Buy and Sell Stock II
**Link** : https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/
```
class Solution {
    public int maxProfit(int[] prices) {
        int result = 0;
        for(int i = 1;i < prices.length;i++){
            if(prices[i] - prices[i - 1] > 0){
                result = result + prices[i] - prices[i - 1];
            }
        }
        return result;
    }
}
```
## [Medium] 55. Jump Game
**Link** : https://leetcode.com/problems/jump-game/submissions/
```
class Solution {
    public boolean canJump(int[] nums) {
        if(nums.length == 1){
            return true;
        }
        int range = 0;
        for(int i = 0;i <= range;i++){
            range = Math.max(range,i + nums[i]);
            if(range >= nums.length - 1){
                return true;
            }
        }
        return false;
    }
}
```
## [Medium] 45. Jump Game II
**Link** : https://leetcode.com/problems/jump-game-ii/description/
```
class Solution {
    public int jump(int[] nums) {
        int result = 0;
        int currentRange = 0;
        int maxRange = 0;
        for(int i = 0;i <= currentRange && currentRange < nums.length - 1;i++){
            maxRange = Math.max(maxRange,i + nums[i]);
            if(i == currentRange){
                currentRange = maxRange;
                result++;
            }
        }
        return result;
        
    }
}
```
## [Easy] 1005. Maximize Sum Of Array After K Negations
**Link** : https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/description/
```
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        if(nums.length == 1){
            return k % 2 == 0 ? nums[0] : -nums[0];
        }
        Arrays.sort(nums);
        int result = 0;
        int index = 0;

        for(int i = 0;i < k;i++){
            if(i < nums.length - 1 && nums[i] < 0){
                nums[index] = -nums[index];
                if(nums[index] >= Math.abs(nums[index+ 1])){
                    
                    index++;
                    
                }
                continue;
            }
            nums[index] = -nums[index];
        }

        for(int i : nums){
            result += i;
        }

        return result;
    }
}
```
## [Medium] 134. Gas Station
**Link** : https://leetcode.com/problems/gas-station/description/
```
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        
        int current = 0;
        int total = 0;
        int start = 0;
        for(int i = 0; i < gas.length;i++){
            total = total + (gas[i] - cost[i]);
            current = current + (gas[i] - cost[i]);
            if(current < 0){
                start = i + 1;
                current = 0;
            }

        }

        return total >= 0 ? start : -1;

    }
}
```
