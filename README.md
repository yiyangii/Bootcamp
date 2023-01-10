# 【Easy】LeetCode 704 Binary Search
Link: https://leetcode.com/problems/binary-search/

在捡起又放下的刷题路上，二分查找已经是老朋友了。
主要思路：二分查找最开始需要设置两个变量L，R （ L为左侧边界，R为右侧边界）接着是一个while循环，循环终止条件通常为判断`while(left < right)`或者是`while(left <= right)` 
在循环中添加变量mid作为L与R的中位数并通过nums[mid]判断与target之间的关系，若是小于target则在循环内更新L，若是大于Target则在循环内更新R。值得注意的是，变量mid通常会写`int mid = left + (right - left) / 2`以避免溢出。

如果是左闭右闭 => [1,1] R与L可以取1 则 `while(left <= right)` 在每次循环中的变量L,R都需要更新 => `L = mid + 1` `R = mid - 1`

如果是左闭右开 => [1,1) L可以取1而R不可以 则 `while(left < right)` 在每次循环中的变量L 需要更新 => `L = mid + 1` `R = mid`



难点：左闭右开与左开右闭

题解：
```
class Solution {
    public int search(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;
        while(left <= right){
            int mid = left + (right - left) / 2;
            if(nums[mid] > target){
                right = mid - 1;
            }else if(nums[mid] < target){
                left = mid + 1;
            }else{
                return mid;
            }
        }
        return -1;
    }
}
```
