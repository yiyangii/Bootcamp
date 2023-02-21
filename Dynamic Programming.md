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

##[Easy] 746. Min Cost Climbing Stairs
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
