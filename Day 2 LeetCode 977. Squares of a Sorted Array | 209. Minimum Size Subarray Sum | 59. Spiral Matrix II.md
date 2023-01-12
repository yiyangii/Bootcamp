# Day 2 LeetCode 977. Squares of a Sorted Array | 209. Minimum Size Subarray Sum | 59. Spiral Matrix II
## [Easy] 977. Squares of a Sorted Array
Link: https://leetcode.com/problems/squares-of-a-sorted-array/

第一次刷到这题偷懒用了Arrays.sort暴力排序一劳永逸，二刷的时候因为想着用快慢指针导致思路错了花了不少时间，其实这题十分简单。

**主要思路** ：双指针一个在左边界一个在右边界，在每一层循环内对比左右边界L,R index对应的平方大小。大的放入新建数组的最后一位并更新L/R以及新建数组最后一位的index。

**难点** ： 这道题理清了思路了解了双指针放置的位置后就非常简单，主要是搞明白两个指针对应的位置。

**题解**：
```
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] result = new int[nums.length];
        int left = 0;
        int right = nums.length - 1;
        int index = nums.length - 1;
        while(index >= 0){
            if(nums[left] * nums[left] < nums[right] * nums[right]){
                result[index] = nums[right] * nums[right];
                index--;
                right--;
            }else{
                result[index] = nums[left] * nums[left];
                index--;
                left++;
            }
        }
        
        return result;
    }
}
```

## [Medium]209. Minimum Size Subarray Sum
**Link** :https://leetcode.com/problems/minimum-size-subarray-sum/description/

第一次看到就想到了滑动窗口，但实际上写了一个暴力解法，一直调整还是超过了time limit最后还是看了题解才恍然大悟。这道题最为精妙的地方还是解法对于窗口的起始点与终止点的处理

**主要思路** ：暴力解法的思路是放置两个指针i和j，i为起始点，j为终止点。解法需要一个嵌套循环用于遍历每一个从起始点i开始到j结束的子数组并且判断它的总和是否超过了target，如果超过了target则更新最小值接着break。这样的解法毫无疑问是O(n^2)的时间复杂度因为要进行一次嵌套数组长度n的循环。

它的改进方法十分巧妙，用双指针left与right来定义子数组的区间，定义一个增加right也就是右边界的循环，每次循环内 `sum += nums[right]` 之后进行一次判断，如果sum值大于或者等于target则进入一个while循环并在循环内进行一次最小值更新的判断操作，在while循环内我们有着当前满足条件`sum >= target`的子数组起始点left与right，我们要做的也十分简单那就是尝试增加左侧边界让子数组长度尽可能减少。

实现这个操作的方法则是`sum -= nums[left]`，如果sum减去nums[左边界]后仍然大于或者等于target意味着我们减少子数组长度成功了，子数组仍然满足`sum >= target`的要求，于是可以在while循环内再次更新最小值。如果sum减去nums[左边界]后小于target则意味着当前已经是当前右边界值所能提供的能满足条件的最小数组了，那么跳出while循环进入下一层for循环。最后得到最小子数组长度。

**难点** ： 这道题如果用暴力解法将会十分容易，但是很明显leetcode要求我们思考的更深入，我觉得最大的难点在于能够想出在单次for循环内实现滑动窗口的操作，这也要求在单循环内更新左边界与右边界的值。希望二刷这道题能够顺利。

**题解**：

```
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int min = Integer.MAX_VALUE;
        int sum = 0;
        int length = 0;
        int left = 0;
        int right = 0;
        for(right = 0;right < nums.length;right++){
            sum += nums[right];
            while(sum >= target){
                length = right - left + 1;
                min = Math.min(min,length);
                sum -= nums[left];
                left++;
            }
        }
        if(min == Integer.MAX_VALUE){
            return 0;
        }else{
            return min;
        }
    }
}
```
