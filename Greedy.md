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
## [Hard] 135. Candy
**Link** : https://leetcode.com/problems/candy/description/
```
class Solution {
    /**
         分两个阶段
         1、起点下标1 从左往右，只要 右边 比 左边 大，右边的糖果=左边 + 1
         2、起点下标 ratings.length - 2 从右往左， 只要左边 比 右边 大，此时 左边的糖果应该 取本身的糖果数（符合比它左边大） 和 右边糖果数 + 1 二者的最大值，这样才符合 它比它左边的大，也比它右边大
    */
    public int candy(int[] ratings) {
        int len = ratings.length;
        int[] candyVec = new int[len];
        candyVec[0] = 1;
        for (int i = 1; i < len; i++) {
            candyVec[i] = (ratings[i] > ratings[i - 1]) ? candyVec[i - 1] + 1 : 1;
        }

        for (int i = len - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) {
                candyVec[i] = Math.max(candyVec[i], candyVec[i + 1] + 1);
            }
        }

        int ans = 0;
        for (int num : candyVec) {
            ans += num;
        }
        return ans;
    }
}
```
## [Easy] 860. Lemonade Change
**Link** : https://leetcode.com/problems/lemonade-change/submissions/899436422/
```
class Solution {
    public boolean lemonadeChange(int[] bills) {
        int five = 0;
        int ten = 0;
        int twenty = 0;

        for(int bill : bills){
            if(bill == 5){
                five++;
            }else if(bill == 10){
                if(five <= 0){
                    return false;
                }
                ten++;
                five--;
            }else if(bill == 20){
                if(five > 0 && ten > 0){
                    five--;
                    ten--;
                    twenty++;
                }else if(five >= 3){
                    five -= 3;
                    twenty++;
                }else{
                    return false;
                }

            }
        }
        return true;
    }
}
```
## [Medium] 452. Minimum Number of Arrows to Burst Balloons
**Link** : https://leetcode.com/problems/minimum-number-of-arrows-to-burst-balloons/description/
```
class Solution {
    public int findMinArrowShots(int[][] points) {
        Arrays.sort(points,(a,b) -> Integer.compare(a[0],b[0]));
        int count = 1;
        for(int i = 1; i < points.length;i++){
            if(points[i][0] > points[i-1][1]){
                count++;
            }else{
                points[i][1] = Math.min(points[i][1],points[i-1][1]);
            }
        }
        return count;
    }
}
```
## [Medium] 435. Non-overlapping Intervals
**Link** : https://leetcode.com/problems/non-overlapping-intervals/description/
```
class Solution {
    public int eraseOverlapIntervals(int[][] intervals) {
        int count = 1;
        Arrays.sort(intervals,(a,b) -> Integer.compare(a[0],b[0]));
        for(int i = 1; i < intervals.length;i++){
            if(intervals[i][0] >= intervals[i - 1][1]){
                count++;
            }else{
                intervals[i][1] = Math.min(intervals[i][1],intervals[i-1][1]);
            }
        }
        return intervals.length - count;
    }
}
```
## [Medium] 763. Partition Labels
**Link** : https://leetcode.com/problems/partition-labels/description/
```
class Solution {
    public List<Integer> partitionLabels(String s) {
        int[] edge = new int[26];
        char[] c = s.toCharArray();
        for(int i = 0;i < c.length;i++){
            edge[c[i] - 'a'] = i;
        }
        List<Integer> result = new ArrayList();

        int index = 0;
        int prev = -1;
        for(int i = 0;i < s.length();i++){
            index = Math.max(index,edge[c[i] - 'a']);
            if(index == i){
                result.add(i - prev);
                prev = i;
            }
        }
        return result;
    }
}
```
## [Medium] 56. Merge Intervals
**Link** : https://leetcode.com/problems/merge-intervals/submissions/900739819/
```
class Solution {
    public int[][] merge(int[][] intervals) {
        Arrays.sort(intervals,(a,b) -> Integer.compare(a[0],b[0]));
        LinkedList<int[]> result = new LinkedList();
        for(int[] interval : intervals){
            if(result.isEmpty() || interval[0] > result.getLast()[1]){
                result.add(interval);
            }else{
                result.getLast()[1] = Math.max(result.getLast()[1],interval[1]);
            }
        }
        return result.toArray(new int[result.size()][]);
    }
}
```
