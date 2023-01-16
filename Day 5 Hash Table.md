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
