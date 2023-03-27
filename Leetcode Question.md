
## [Easy] 1365. How Many Numbers Are Smaller Than the Current Number
```
class Solution {
    public int[] smallerNumbersThanCurrent(int[] nums) {
        int[] result = new int[nums.length];
        Arrays.sort(nums);
        for(int i = 0;i < nums.length;i++){
            for(int j = i;j < nums.length;j++){
                if(nums[j] < nums[i]){
                    result[i]++;
                }
            }
        } 
        return result;  
    }
}
```
## [Easy] 941. Valid Mountain Array
```
class Solution {
    public boolean validMountainArray(int[] arr) {
        if(arr.length < 3){
            return false;
        }
        int left = 0;
        int right = arr.length - 1;;
        while(left < arr.length - 1 && arr[left] < arr[left + 1]){
            left ++;
        }
        while(right > 0 &&  arr[right] < arr[right - 1]){
            right--;

        }
        if(right == left && left != 0 && right != arr.length - 1){
            return true;
        }
        return false;
    }
}
```
