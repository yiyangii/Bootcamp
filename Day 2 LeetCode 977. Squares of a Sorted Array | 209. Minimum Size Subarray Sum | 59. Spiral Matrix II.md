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


