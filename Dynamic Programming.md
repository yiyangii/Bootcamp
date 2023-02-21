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

