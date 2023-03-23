## [Easy] 509. Fibonacci Number
**Link** : https://leetcode.com/problems/fibonacci-number/description/
```
class Solution {
    public int fib(int n) {
        int[] dp = new int[n + 1];
        if(n == 0 || n == 1){
            return n;
        }
        dp[0] = 0;
        dp[1] = 1;
        for(int i = 2; i <= n;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }

        return dp[n];
    }
}
```
## [Easy] 70. Climbing Stairs
**Link** : https://leetcode.com/problems/climbing-stairs/
```
class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;

        for(int i = 2;i <=n;i++){
            dp[i] = dp[i-1] + dp[i-2];
        }
        return dp[n];
    }
}
```

## [Easy] 746. Min Cost Climbing Stairs
**Link** : https://leetcode.com/problems/min-cost-climbing-stairs/
```
class Solution {
    public int minCostClimbingStairs(int[] cost) {
       int[] dp = new int[cost.length + 2];
        dp[0] = 0;
        dp[1] = 0;
        for(int i = 2;i <= cost.length;i++){
            dp[i] = Math.min(dp[i-1] + cost[i-1],dp[i-2] + cost[i-2]);
        }
        return dp[cost.length];
    }
}
```
## [Medium] 62. Unique Paths
**Link** : https://leetcode.com/problems/unique-paths/
```
class Solution {
    public int uniquePaths(int m, int n) {
        int[][] grid = new int[m][n];
        for(int i = 0; i < m;i++){
            grid[i][0] = 1;
        }
        for(int i = 0;i < n;i++){
            grid[0][i] = 1;
        }
        for(int i = 1;i < m;i++){
            for(int j = 1;j < n;j++){
                grid[i][j] = grid[i - 1][j] + grid[i][j-1];
            }
        }
        return grid[m  - 1][n - 1];  
    }
}
```
## [Medium] 63. Unique Paths II
**Link** : https://leetcode.com/problems/unique-paths-ii/description/
```
class Solution {
    public int uniquePathsWithObstacles(int[][] obstacleGrid) {
        int n = obstacleGrid[0].length;

        int m = obstacleGrid.length;
        int[][] grid = new int[m][n];

        if(obstacleGrid[0][0] == 1 || obstacleGrid[m - 1][n - 1] == 1){
            return 0;
        }

        for(int i = 0;i < m && obstacleGrid[i][0] == 0;i++){
            grid[i][0] = 1;
        }
        
        
        for(int i = 0;i < n && obstacleGrid[0][i] == 0;i++){
            grid[0][i] = 1;
        }



        for(int i = 1;i < m;i++){
            for(int j = 1;j < n;j++){
                if(obstacleGrid[i][j] == 0){
                    grid[i][j] = grid[i - 1][j] + grid[i][j - 1];
                }else{
                    grid[i][j] = 0;
                }
            }
        }
        
        return grid[m-1][n-1];
    }
}
```
## [Medium] 343. Integer Break
**Link** : https://leetcode.com/problems/integer-break/description/
```
class Solution {
    public int integerBreak(int n) {
        int[] dp = new int[n + 1];
        dp[2] = 1;
        for(int i = 3;i <= n;i++){
            for(int j = 1; j <= i - j;j++){
                dp[i] = Math.max(dp[i],Math.max(dp[i - j] * j,(i - j) * j));
            }
        }
        return dp[n];

    }
}
```
## [Medium] 96. Unique Binary Search Trees
**Link** https://leetcode.com/problems/unique-binary-search-trees/description/
```
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;  
        
        for(int i = 2;i <= n;i++){
            for(int j = 1;j <= i;j++){
                dp[i] = dp[i] + dp[j - 1] * dp[i-j];
            }    
        }
        return dp[n];
    }
}
```
## [Medium] 416. Partition Equal Subset Sum
**Link** : https://leetcode.com/problems/partition-equal-subset-sum/description/
```
class Solution {
    public boolean canPartition(int[] nums) {
        if(nums == null || nums.length == 0){
            return false;
        }
        int sum = 0;
        for(int i : nums){
            sum += i;
        }

        if(sum % 2 != 0){
            return false;
        }
        int target = sum / 2;
        int[] dp = new int[target + 1];

        for(int i = 0;i < nums.length;i++){
            for(int j = target; j >= nums[i];j--){
                dp[j] = Math.max(dp[j],Math.max(dp[j],dp[j - nums[i]] + nums[i]));
            }
        }
        return dp[target] == target;
    }
}
```
## [Medium] 416. Partition Equal Subset Sum
**Link** : https://leetcode.com/problems/partition-equal-subset-sum/description/
```
class Solution {
    public boolean canPartition(int[] nums) {
        if(nums == null || nums.length == 0){
            return false;
        }
        int sum = 0;
        for(int i : nums){
            sum += i;
        }

        if(sum % 2 != 0){
            return false;
        }
        int target = sum / 2;
        int[] dp = new int[target + 1];

        for(int i = 0;i < nums.length;i++){
            for(int j = target; j >= nums[i];j--){
                dp[j] = Math.max(dp[j],Math.max(dp[j],dp[j - nums[i]] + nums[i]));
            }
        }
        return dp[target] == target;
    }
}
```
## [Medium] 1049. Last Stone Weight II
**Link** : https://leetcode.com/problems/last-stone-weight-ii/description/
```
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int sum = 0;
        for(int i : stones){
            sum += i;
        }
        int target = sum / 2;
        int left = sum - target;
        int[] dp = new int[target + 1];
        for(int i = 0;i < stones.length;i++){
            for(int j = target;j >= stones[i];j--){
                dp[j] = Math.max(dp[j],dp[j - stones[i]] + stones[i]);
            }
        }
        return sum - dp[target] - dp[target];
    }
}
```
## [Medium] 494. Target Sum
**Link** : https://leetcode.com/problems/target-sum/description/
```
class Solution {

    public int findTargetSumWays(int[] nums, int target) {
        int sum = 0;
        for(int i : nums){
            sum += i;
        }

        if((sum + target) % 2 != 0){
            return 0; 
        }
        if(target < 0 && sum < - target){
            return 0;
        }

        int size = (sum + target) / 2;
        if(size < 0){
            size = -size;
        }
        int[] dp = new int[size + 1];
        dp[0] = 1;
        for(int i = 0;i < nums.length;i++){
            for(int j = size;j >= nums[i];j--){
                dp[j] += dp[j - nums[i]];
            }
        }
        return dp[size];
    }
}
```
## [Medium] 474. Ones and Zeroes
**Link** : https://leetcode.com/problems/ones-and-zeroes/description/
```
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int[][] dp = new int[m + 1][n + 1];
        int one;
        int zero;
        for(String s : strs){
            zero = 0;
            one = 0;
            for(char c : s.toCharArray()){
                if(c == '1'){
                    one++;
                }else{
                    zero++;
                }
            }

            for(int i = m; i >= zero;i--){
                for(int j = n; j >= one;j--){
                    dp[i][j] = Math.max(dp[i][j],dp[i - zero][j - one] + 1);
                }
            }
        }
        return dp[m][n];
    }
}
```
## [Medium] 518. Coin Change II
**Link** : https://leetcode.com/problems/coin-change-ii/description/
```
class Solution {
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        for(int i = 0;i < coins.length;i++){
            for(int j = coins[i]; j <= amount;j++){
                dp[j] += dp[j - coins[i]];
            }
        }
        return dp[amount];
        
    }
}
```
## [Medium] 377. Combination Sum IV
**Link** : https://leetcode.com/problems/combination-sum-iv/description/
```
class Solution {
    public int combinationSum4(int[] nums, int target) {
        int[] dp = new int[target + 1];
        dp[0] = 1;
        for (int i = 0; i <= target; i++) {
            for (int j = 0; j < nums.length; j++) {
                if (i >= nums[j]) {
                    dp[i] += dp[i - nums[j]];
                }
            }
        }
        return dp[target];
    }
}
```
## [Easy] 70. Climbing Stairs
 **Link** : https://leetcode.com/problems/climbing-stairs/description/
 ```
 class Solution {
    public int climbStairs(int n) {
        int[] dp = new int[n + 1];
        int[] weight = new int[]{1,2};
        dp[0] = 1;
        for(int i = 0;i <= n;i++){
            for(int j = 0; j < weight.length;j++){
                if(i >= weight[j]){
                    dp[i] += dp[i - weight[j]];
                } 
            }
        }
        return dp[n];
    }
}
 ```
 ## [Medium] 322. Coin Change
 **Link** : https://leetcode.com/problems/coin-change/description/
 ```
 class Solution {
    public int coinChange(int[] coins, int amount) {
        int max = Integer.MAX_VALUE;
        
        int[] dp = new int[amount + 1];
        for(int i = 0;i < dp.length;i++){
            dp[i] = max;
        }
        dp[0] = 0;
        for(int i = 0;i < coins.length;i++){
            for(int j = coins[i];j <= amount;j++){
                if(dp[j - coins[i]] != max){
                    dp[j] = Math.min(dp[j],dp[j - coins[i]] + 1);
                }
            }
        }

        if(dp[amount] == max){
            return -1;
        }
        return dp[amount];
    }
}
 ```
 ## [Medium]279. Perfect Squares
 **Link** : https://leetcode.com/problems/perfect-squares/submissions/906140825/
 ```
 class Solution {
    public int numSquares(int n) {
        int max = Integer.MAX_VALUE;
        
        int[] dp = new int[n + 1];
        for(int i = 0;i < dp.length;i++){
            dp[i] = max;
        }
        dp[0] = 0;
        for(int i = 1;i * i <= n;i++){
            for(int j = i * i;j <= n;j++){
                if(dp[j - i * i] != max){
                    dp[j] = Math.min(dp[j],dp[j - i * i] + 1);
                }
            }
        };
        return dp[n];
        
    }
}
 ```
 ## [Medium] 139. Word Break
 **Link** : https://leetcode.com/problems/word-break/
 ```
 class Solution {
    public boolean wordBreak(String s, List<String> wordDict) {
        HashSet<String> set = new HashSet(wordDict);
        boolean[] dp = new boolean[s.length() + 1];
        dp[0] = true;
        for(int i = 1;i <= s.length();i++){
            for(int j = 0;j < i && !dp[i];j++){
                if(set.contains(s.substring(j,i)) && dp[j]){
                    dp[i] = true;
                }
            }
        }
        return dp[s.length()];
    }
}  
 ```
 ## [Medium] 198. House Robber
**Link** : https://leetcode.com/problems/house-robber/description/
```
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 0){
            return 0;
        }

        if(nums.length == 1){
            return nums[0];
        }
        
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        
        dp[1] = Math.max(nums[0],nums[1]);
        for(int i = 2;i < nums.length;i++){
            dp[i] = Math.max(dp[i - 1],dp[i - 2] + nums[i]);
        }
        return dp[nums.length - 1];
        
    }
}
```
## [Medium] 213. House Robber II
**Link** : https://leetcode.com/problems/house-robber-ii/description/
```
class Solution {
    public int rob(int[] nums) {
        if(nums.length == 0){
            return 0;
        }
        if(nums.length == 1){
            return nums[0];
        }

        return Math.max(maxRob(nums,0,nums.length - 2),maxRob(nums,1,nums.length - 1));
    }

    public int maxRob(int[] nums,int start,int end){
        if(start == end){
            return nums[start];
        }
        int[] dp = new int[nums.length];
        dp[start] = nums[start];
        
        dp[start + 1] = Math.max(nums[start],nums[start + 1]);
        for(int i = start + 2;i <= end;i++){
            dp[i] = Math.max(dp[i - 1],dp[i - 2] + nums[i]);
        }
        return dp[end];

    }
}
```
## [Medium] 337. House Robber III
**Link** : https://leetcode.com/problems/house-robber-iii/description/
```
class Solution {
    public int rob(TreeNode root) {
        int[] ans = recursion(root);
        return Math.max(ans[0],ans[1]);
    }

    public int[] recursion(TreeNode root){
        int[] result = new int[2];
        if(root == null){
            return result;
        }

        int[] left = recursion(root.left);
        int[] right = recursion(root.right);

        result[0] = Math.max(left[0],left[1]) + Math.max(right[0],right[1]);
        result[1] = root.val + right[0] + left[0];

        return result;
    }
}
```
## [Medium] 121. Best Time to Buy and Sell Stock
**Link** ：https://leetcode.com/problems/best-time-to-buy-and-sell-stock/description/
```
class Solution {
    public int maxProfit(int[] prices) {
        int[] dp = new int[2];
        dp[0] = -prices[0];
        dp[1] = 0;
        for(int i = 1;i < prices.length;i++){
            dp[0] = Math.max(dp[0],-prices[i]);
            dp[1] = Math.max(dp[1],dp[0] + prices[i]);
        }
        return dp[1];
        
    }
}
```
## [Medium] 121. Best Time to Buy and Sell Stock
**Link** ：https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/description/
```
class Solution {
    public int maxProfit(int[] prices) {
        int[] dp = new int[2];
        // 0表示持有，1表示卖出
        dp[0] = -prices[0];
        dp[1] = 0;
        for(int i = 1; i <= prices.length; i++){
            // 前一天持有; 既然不限制交易次数，那么再次买股票时，要加上之前的收益
            dp[0] = Math.max(dp[0], dp[1] - prices[i-1]);
            // 前一天卖出; 或当天卖出，当天卖出，得先持有
            dp[1] = Math.max(dp[1], dp[0] + prices[i-1]);
        }
        return dp[1];
    }
}
```

## [Hard] 123. Best Time to Buy and Sell Stock III
**Link** : https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iii/description/
```
class Solution {
    public int maxProfit(int[] prices) {
        int[][] dp = new int[prices.length][4];
        dp[0][0] = -prices[0];
        dp[0][1] = 0;
        dp[0][2] = -prices[0];
        dp[0][3] = 0;
        for(int i = 1;i < prices.length;i++){
            dp[i][0] = Math.max(dp[i-1][0],-prices[i]); 
            dp[i][1] = Math.max(dp[i - 1][1],dp[i - 1][0] + prices[i]);
            dp[i][2] = Math.max(dp[i - 1][2],dp[i - 1][1] - prices[i]);
            dp[i][3] = Math.max(dp[i - 1][3],dp[i - 1][2] + prices[i]);
        }

        return dp[prices.length - 1][3];
    }
}
```
## [Hard] 188. Best Time to Buy and Sell Stock IV
**Link** : https://leetcode.com/problems/best-time-to-buy-and-sell-stock-iv/description/
```
class Solution {
    public int maxProfit(int k, int[] prices) {
        int[][] dp = new int[prices.length][2 * k + 1];
        for(int i = 1; i < 2 * k;i += 2){
            dp[0][i] = -prices[0];
        }

        for(int i = 1;i < prices.length;i++){
            for(int j = 0;j < k * 2 - 1;j += 2){
                dp[i][j + 1] = Math.max(dp[i - 1][j + 1],dp[i - 1][j] - prices[i]);
                dp[i][j + 2] = Math.max(dp[i - 1][j + 2],dp[i - 1][j + 1] + prices[i]);
            }
        }
        return dp[prices.length - 1][k * 2];
    }
}
```
## [Medium] 309. Best Time to Buy and Sell Stock with Cooldown
**Link** : https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-cooldown/description/
```
class Solution {
    public int maxProfit(int[] prices) {
        if (prices == null || prices.length < 2) {
            return 0;
        }
        int[][] dp = new int[prices.length][4];
        dp[0][0] = -prices[0];
        dp[0][1] = 0;
        dp[0][2] = 0;
        dp[0][3] = 0;
        for(int i = 1;i < prices.length;i++){
            dp[i][0] = Math.max(dp[i - 1][0],Math.max(dp[i - 1][3] - prices[i],dp[i - 1][1] - prices[i]));
            dp[i][1] = Math.max(dp[i - 1][1],dp[i - 1][3]);
            dp[i][2] = dp[i - 1][0] + prices[i];
            dp[i][3] = dp[i - 1][2];
        }

        return Math.max(dp[prices.length - 1][3],Math.max(dp[prices.length - 1][2],dp[prices.length - 1][1]));
    }
}
```
## [Medium]714. Best Time to Buy and Sell Stock with Transaction Fee
**Link** : https://leetcode.com/problems/best-time-to-buy-and-sell-stock-with-transaction-fee/
```
class Solution {
    public int maxProfit(int[] prices, int fee) {
        int[][] dp = new int[prices.length][2];
        dp[0][0] = -prices[0];
        dp[0][1] = 0;
        for(int i = 1;i < prices.length;i++){
            dp[i][0] = Math.max(dp[i - 1][0],dp[i - 1][1] - prices[i]);
            dp[i][1] = Math.max(dp[i - 1][1],dp[i - 1][0] + prices[i] - fee);
        }
        return Math.max(dp[prices.length - 1][0],dp[prices.length - 1][1]);
    }
}
```
##[Medium] 300. Longest Increasing Subsequence
**Link** : https://leetcode.com/problems/longest-increasing-subsequence/description/
```
class Solution {
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp,1);
        for(int i = 0;i < nums.length;i++){
            for(int j = 0; j < i;j++){
                if(nums[i] > nums[j]){
                    dp[i] = Math.max(dp[i],dp[j] + 1);
                }
            }
        }
        int res = 0;
        for(int i: dp){
            res = Math.max(res,i);
        }
        return res;
    }
}
```
## [Easy] 674. Longest Continuous Increasing Subsequence
**Link** : https://leetcode.com/problems/longest-continuous-increasing-subsequence/description/
```
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp,1);
        for(int i = 1;i < nums.length;i++){
            if(nums[i] > nums[i - 1]){
                dp[i] = dp[ i - 1] + 1;
            }  
        }
        int result = 0;
        for(int i : dp){
            result = Math.max(result,i);
        }
        return result; 
    }
}
```
## [Medium]718. Maximum Length of Repeated Subarray
**Link** : https://leetcode.com/problems/maximum-length-of-repeated-subarray/description/
```
class Solution {
    public int findLength(int[] nums1, int[] nums2) {
        int[][] dp = new int[nums1.length + 1][nums2.length + 1];
        int result = 0;
        for(int i = 1;i < nums1.length + 1;i++){
            for(int j = 1;j < nums2.length + 1;j++){
                if(nums1[i - 1] == nums2[j - 1]){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                    result = Math.max(dp[i][j],result);
                }
            }
        }
        return result;

    }
}
```
## [Medium] 1143. Longest Common Subsequence
```
class Solution {

    public int longestCommonSubsequence(String text1, String text2) {
        int[][] dp = new int[text1.length() + 1][text2.length()+ 1];
        for(int i = 1;i <= text1.length();i++){
            char char1 = text1.charAt(i - 1);
            for(int j = 1;j <= text2.length();j++){
                char char2 = text2.charAt(j - 1);
                if(char1 == char2){
                    dp[i][j] = dp[i-1][j-1] + 1;
                }else{
                    dp[i][j] = Math.max(dp[i - 1][j],dp[i][j - 1]);
                }
            }
        }
        return dp[text1.length()][text2.length()]; 
    }   
}
```
## [Medium] 1035. Uncrossed Lines
```
class Solution {
    public int maxUncrossedLines(int[] nums1, int[] nums2) {
        int[][] dp = new int[nums1.length + 1][nums2.length +  1];
        for(int i = 1;i <= nums1.length;i++){
            int num1 = nums1[i - 1];
            for(int j = 1;j <= nums2.length;j++){
                int num2 = nums2[j - 1];
                if(num1 == num2){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }else{
                    dp[i][j] = Math.max(dp[i - 1][j],dp[i][j - 1]);
                }
            }
        }
        return dp[nums1.length][nums2.length];

    }
}
```
## [Medium] 53. Maximum Subarray
```
class Solution {
    public int maxSubArray(int[] nums) {
        if(nums.length == 0){
            return 0;
        }
        int[] dp = new int[nums.length];
        int result = nums[0];
        dp[0] = nums[0];
        for(int i = 1;i < nums.length;i++){
            dp[i] = Math.max(dp[i - 1] + nums[i],nums[i]);
            if(result < dp[i]){
                result = dp[i];
            }
        }
        return result;
    }
}
```

## [Easy] 392. Is Subsequence
```
class Solution {
    public boolean isSubsequence(String s, String t) {
        int[][] dp = new int[s.length() + 1][t.length() + 1];
        for(int i = 1;i <= s.length();i++){
            char char1 = s.charAt(i - 1);
            for(int j = 1;j <= t.length();j++){
                char char2 = t.charAt(j - 1);
                if(char1 == char2){
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                }else{
                    dp[i][j] = dp[i][j - 1];
                }
            }
        }
        if(dp[s.length()][t.length()] == s.length()){
            return true;
        }
        return false;
        
    }
}
```
## [Hard] 115. Distinct Subsequences
```
class Solution {
    public int numDistinct(String s, String t) {
        int[][] dp = new int[s.length() + 1][t.length() + 1];
        for (int i = 0; i < s.length() + 1; i++) {
            dp[i][0] = 1;
        }
        for(int i = 1;i <= s.length();i++){
            char char1 = s.charAt(i - 1);
            for(int j = 1;j <= t.length();j++){
                char char2 = t.charAt(j - 1);
                if(char1 == char2){
                    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
                }else{
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        return dp[s.length()][t.length()];
    }
}
```
## [Medium] 583. Delete Operation for Two Strings
```
class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length() + 1][word2.length() + 1];
        for(int i = 0;i <= word1.length();i++){
            dp[i][0] = i;
        }
        for(int i = 0;i <= word2.length();i++){
            dp[0][i] = i;
        }
        for(int i = 1;i <= word1.length();i++){
            char char1 = word1.charAt(i - 1);
            for(int j = 1;j <= word2.length();j++){
                char char2 = word2.charAt(j - 1);
                if(char1 == char2){
                    dp[i][j] = dp[i - 1][j - 1];
                }else{
                    dp[i][j] = Math.min(dp[i - 1][j] + 1,dp[i][j - 1] + 1);
                }
            }
        }
        return dp[word1.length()][word2.length()];
    }
}
```
## [Hard] 72. Edit Distance
```
class Solution {
    public int minDistance(String word1, String word2) {
        int[][] dp = new int[word1.length() + 1][word2.length() + 1];
        for(int i = 0;i <= word1.length();i++){
            dp[i][0] = i;
        }
        for(int i = 0;i <= word2.length();i++){
            dp[0][i] = i;
        }
        for (int i = 1; i <= word1.length(); i++) {
        for (int j = 1; j <= word2.length(); j++) {

            if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                dp[i][j] = dp[i - 1][j - 1];
            } else {
                dp[i][j] = Math.min(Math.min(dp[i - 1][j - 1], dp[i][j - 1]), dp[i - 1][j]) + 1;
            }
        }
    }
    return dp[word1.length()][word2.length()];
    }
}
```

## [Medium] 647. Palindromic Substrings
```
class Solution {
    public int countSubstrings(String s) {
        int len = s.length();
        int result = 0;
        if(s == null || len < 1){
            return 0;
        }
        boolean[][] dp = new boolean[s.length()][s.length()];
        for(int j = 0;j < len;j++){
            for(int i = 0;i <= j; i++){
                if(s.charAt(i) == s.charAt(j)){
                    if(j - i < 3){
                        dp[i][j] = true;
                    }else{
                        dp[i][j] = dp[i + 1][j - 1];
                    }
                }else{
                    dp[i][j] = false;
                }
            }
        }
        for (int i = 0; i < len; i++) {
            for (int j = 0; j < len; j++) {
                if (dp[i][j]) result++;
            }
        }
        return result;
    }
}
```
# [Medium] 516. Longest Palindromic Subsequence
```
class Solution {
    public int longestPalindromeSubseq(String s) {
        int[][] dp = new int[s.length() + 1][s.length() + 1];
        for(int i = s.length() - 1; i >= 0;i--){
            dp[i][i] = 1;
            for(int j = i + 1;j < s.length();j++){
                if(s.charAt(i) == s.charAt(j)){
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                }else{
                    dp[i][j] = Math.max(dp[i + 1][j],Math.max(dp[i][j - 1],dp[i][j]));
                }
            }
        }
        return dp[0][s.length() - 1];
        
    }
}
```
## [Hard] 42. Trapping Rain Water
```
class Solution {
    public int trap(int[] height){
        int size = height.length;

        if (size <= 2) return 0;

        // in the stack, we push the index of array
        // using height[] to access the real height
        Stack<Integer> stack = new Stack<Integer>();
        stack.push(0);

        int sum = 0;
        for (int index = 1; index < size; index++){
            int stackTop = stack.peek();
            if (height[index] < height[stackTop]){
                stack.push(index);
            }else if (height[index] == height[stackTop]){
                // 因为相等的相邻墙，左边一个是不可能存放雨水的，所以pop左边的index, push当前的index
                stack.pop();
                stack.push(index);
            }else{
                //pop up all lower value
                int heightAtIdx = height[index];
                while (!stack.isEmpty() && (heightAtIdx > height[stackTop])){
                    int mid = stack.pop();

                    if (!stack.isEmpty()){
                        int left = stack.peek();

                        int h = Math.min(height[left], height[index]) - height[mid];
                        int w = index - left - 1;
                        int hold = h * w;
                        if (hold > 0) sum += hold;
                        stackTop = stack.peek();
                    }
                }
                stack.push(index);
            }
        }

        return sum;
    }
}
```
