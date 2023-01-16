## 【Easy】LeetCode 242. Valid Anagram
**link** : https://leetcode.com/problems/valid-anagram/description/

**题解** : 

```
class Solution {
    public boolean isAnagram(String s, String t) {
        int[] map = new int[26];
        for(char c : s.toCharArray()){
            map[c - 'a']++;
        }

        for(char c : t.toCharArray()){
            map[c - 'a']--;
        }

        for(int i = 0;i < map.length;i++){
            if(map[i] != 0){
                return false;
            } 
        }
        return true;
    }
}
```

## 【Easy】LeetCode 349. Intersection of Two Arrays
**link** : https://leetcode.com/problems/intersection-of-two-arrays/

**题解** : 

```
class Solution {
    public int[] intersection(int[] nums1, int[] nums2) {
        Set<Integer> set = new HashSet();
        for(int i : nums1){
            if(!set.contains(i)){
                set.add(i);
            }
        }
        Set<Integer> result = new HashSet();;
    
        for(int i : nums2){
            if(set.contains(i)){
            
                result.add(i);
            }
        }

        int[] resultInt = new int[result.size()];
        int count = 0;
        for(int i : result){
            resultInt[count] = i;
            count++;
        } 
        return resultInt;
    }
}
```


## 【Easy】LeetCode 202. Happy Number

**link** : https://leetcode.com/problems/happy-number/description/

**题解** : 

```
class Solution {
    public boolean isHappy(int n) {
        
        Set<Integer> sumSet = new HashSet();
        int sum = getSum(n);
        while(sum != 1 && !sumSet.contains(sum)){
            sumSet.add(sum);
            sum = getSum(sum);
            
            if(sum == 1){
                return true;
            }
        }
        return sum == 1;
    }

    public int getSum(int n){
        int sum = 0;
        while(n > 0){
            int i = n % 10;
            sum = sum + i * i;
            n = n / 10;
        }
        return sum;

    }
}
```
## 【Easy】LeetCode 1. Two Sum

**link** : https://leetcode.com/problems/two-sum/

**题解** : 

```
class Solution {
    public int[] twoSum(int[] nums, int target) {
        if(nums == null){
            return nums;
        }
        int[] result = new int[2];
        Map<Integer,Integer> map = new HashMap();
        for(int i = 0;i < nums.length;i++){
            
            if(map.containsKey(nums[i])){
                
                result[0] = map.get(nums[i]);
                result[1] = i;
                return result;
                
            }
            
            map.put(target - nums[i],i);
        }
        return nums;
        
    }
}
```
## 【Medium】LeetCode 454. 4Sum II

**link** : https://leetcode.com/problems/4sum-ii/description/

**思路** : 本题是四数之和，求得是四个数组中的数字相加等于0的情况有多少,因此不需要考虑去重的情况。那么问题就很简单了和two sum类似。将两个数组两两相加，将两个数的和放入hash table，并且记录它出现的次数。记录次数是为了之后3和4数组相加的时候，如果加上hash table中的数能够等于0，那么结果只需要加上它出现的次数即可。

举个例子，1 + 1 = 2 - 0 + 2 = 2， nums3 + nums4 = -2.出现2的情况有两次，那么在hash table中它的次数被记录了下来，和nums3 + 4创造组合能够创造两个组合。 `result = result + 2`

**题解** :
```
class Solution {
    public int fourSumCount(int[] nums1, int[] nums2, int[] nums3, int[] nums4) {
        Map<Integer,Integer> map = new HashMap();
        for(int i : nums1){
            for(int j : nums2){
                int sum = i + j;
                if(map.containsKey(sum)){
                    map.put(sum,map.get(sum) + 1);
                }else{
                    map.put(sum,1);
                }
            }
        }
        int result = 0;
        for(int i : nums3){
            for(int j : nums4){
                int sum = i+ j;
                if(map.containsKey(0 - sum)){
                    result = result + map.get(0 - sum);
                }
            }
        }
        return result;
    } 
}


```

