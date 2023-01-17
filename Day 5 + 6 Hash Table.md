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
## 【Easy】LeetCode 383. Ransom Note

**link** : https://leetcode.com/problems/ransom-note/description/

**思路** : 题目求的是ransomNote中是否每个字母都可以在magazine中找到，那么就是遍历整个magazine，将每个字母加入hash table，接着遍历整个ransomNote，找到table中对应的字母，如果字母不在hash table中代表false，如果有就看出现的次数，次数小于0则返回false；

**题解** :

```

class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        int[] map = new int[26];

        

        for(char c : magazine.toCharArray()){
            map[c - 'a']++;
        }

        for(char c : ransomNote.toCharArray()){
            map[c - 'a']--;
        }

        for(int i : map){
            if(i < 0){
                return false;
            }
        }
        return true;
    }
}
```

```
class Solution {
    public boolean canConstruct(String ransomNote, String magazine) {
        Map<Character,Integer> map = new HashMap();

        for(char c : magazine.toCharArray()){
            if(!map.containsKey(c)){
                map.put(c,1);
            }else{
                map.put(c,map.get(c) + 1);
            }
        }

        for(char c : ransomNote.toCharArray()){
            if(!map.containsKey(c)){
                return false;
            }
            if(map.containsKey(c)){
                map.put(c,map.get(c) - 1);
                if(map.get(c) < 0){
                    return false;
                }
            }
        }
        return true;
    }
}
```

## 【Medium】LeetCode 15. 3Sum

**link** : https://leetcode.com/problems/3sum/description/

**思路** : 虽然在hash table里，但是其实是双指针。首先先sort一下数组让它从小到大排列。这样遍历的时候如果发现当前数值大于0代表着后面无论如何，结果都会大于0，可以直接返回。在这里，i作为每次循环的起始点，l和r分别是从i开始的第一位数和最后一位数。由于i之前的结果已经遍历过了因此不需要重新考虑。接下来进行一个while循环，当l大于r时终止，由于l不能等于r因为是三个数的和。如果三数之和等于0则将当前的三个数字加入result，接着去重，之后l与r移动到下一个新数字上。同样的去重操作也需要出现在i上，可以在for循环中进行i的去重。

**题解** :

```
class Solution {
    public List<List<Integer>> threeSum(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        int length = nums.length;
        Arrays.sort(nums);
        for(int i = 0;i < length;i++){
            int l = i + 1;
            int r = length - 1;
            if(i > 0 && nums[i] == nums[i - 1]){
                continue;
            }
            while(l < r){
                int sum = nums[i] + nums[l] + nums[r];
                if(nums[i] > 0){
                    break;
                }
                if(sum > 0){
                    r--;
                }else if(sum < 0){
                    l++;
                }else{
                    List<Integer> temp = new ArrayList();
                    temp.add(nums[i]);
                    temp.add(nums[l]);
                    temp.add(nums[r]);
                    result.add(temp);
                    
                    while(l < r && nums[l] == nums[l + 1]){
                        l++;
                    }
                    while(l < r && nums[r] == nums[r - 1]){
                        r--;
                    }
                    l++;
                    r--;
               }
            }
        }
        return result;
        
    }
}
```



## 【Medium】LeetCode 18. 4Sum

**link** : https://leetcode.com/problems/4sum/description/

**思路** : 跟三数之和类似，多加了一层for循环用于循环第二个数，剩下的两个数为l与r。值得注意的是，sum有可能是超过Integer.max的数因此需要为long。

**题解** :

```
class Solution {
    public List<List<Integer>> fourSum(int[] nums, int target) {

       
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList();

        for(int i = 0;i < nums.length;i++){
            
            if(i > 0 && nums[i] == nums[i-1]){
                continue;
            }
            for(int j = i + 1;j < nums.length;j++){

                
                if(j > i + 1 && nums[j] == nums[j-1]){
                    continue;
                }

                int l = j + 1;
                int r = nums.length - 1;

                while(l < r){
                    long sum = (long )nums[i] + nums[j] + nums[l] + nums[r];
                    if(sum == target){
                        List<Integer> temp = new ArrayList();
                        temp.add(nums[i]);
                        temp.add(nums[j]);
                        temp.add(nums[l]);
                        temp.add(nums[r]);
                        result.add(temp);

                        while(l < r && nums[l] == nums[l + 1]){
                            l++;
                        }

                        while(l < r && nums[r] == nums[r - 1]){
                            r--;
                        }
                        l++;
                        r--;
                    }else if(sum > target){
                        r--;
                    }else{
                        l++;
                    }
                }
            }
        }
        return result;
        
    }
}
```
