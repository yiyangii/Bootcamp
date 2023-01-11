## 今日学习时常2小时，第一次尝试记录自己的刷题花了不少时间
今日素材：
https://programmercarl.com/%E6%95%B0%E7%BB%84%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.html
https://programmercarl.com/0704.%E4%BA%8C%E5%88%86%E6%9F%A5%E6%89%BE.html
https://programmercarl.com/0027.%E7%A7%BB%E9%99%A4%E5%85%83%E7%B4%A0.html
https://www.bilibili.com/video/BV1fA4y1o715/?spm_id_from=333.788

# 【Easy】LeetCode 704 Binary Search
**Link**: https://leetcode.com/problems/binary-search/

在捡起又放下的刷题路上，二分查找已经是老朋友了。

**主要思路**：二分查找最开始需要设置两个变量L，R （ L为左侧边界，R为右侧边界）接着是一个while循环，循环终止条件通常为判断`while(left < right)`或者是`while(left <= right)` 
在循环中添加变量mid作为L与R的中位数并通过nums[mid]判断与target之间的关系，若是小于target则在循环内更新L，若是大于Target则在循环内更新R。值得注意的是，变量mid通常会写`int mid = left + (right - left) / 2`以避免溢出。

如果是左闭右闭 => [1,1] R与L可以取1 则 `while(left <= right)` 在每次循环中的变量L,R都需要更新 => `L = mid + 1` `R = mid - 1` 

nums[mid] > target : mid所在index不可取，在下一次循环中若取mid作为右边界R则违反左闭右闭法则 -> nums[1] > target,则1不可取，R = 1则[1,1]不成立 因此需要更新L,R -> R = R - 1，L = L + 1

如果是左闭右开 => [1,1) L可以取1而R不可以 则 `while(left < right)` 在每次循环中的变量L 需要更新 => `L = mid + 1` `R = mid`



**难点**：左闭右开与左开右闭



**步骤**：

- 初始化L,R两个边界变量
- 添加while循环并设置循环终止条件
- 循环内初始化中位数mid
- 根据逻辑语句更新L,R
- 返回结果

**题解**：
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
# 【Easy】LeetCode 27 Remove Element
**Link**: https://leetcode.com/problems/remove-element/description/

理解了大概思路以后几分钟就做出来了，主要是明白题意不能直接创建新数组然后赋值。

**难点**：理解快慢指针的任务，慢指针的每次增加都意味着快指针找到目标元素并与当前快指针所处的位置元素进行替换，快指针负责遍历数组找到目标元素。

**主要思路**: 经典双指针问题，通过快慢指针实现对数组的修改。慢指针用于修改数组，快指针寻找非目标元素。
**题解**：
```
class Solution {
    public int removeElement(int[] nums, int val) {
        int fast = 0;
        int slow = 0;
        for(fast = 0;fast < nums.length;fast++){
            if(nums[fast] != val){
                nums[slow] = nums[fast];
                slow = slow + 1;
            }
        }
        return slow;
    }
}
```
