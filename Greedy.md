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
