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
