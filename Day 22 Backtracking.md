## [Medium] 77. Combinations
**Link** : https://leetcode.com/problems/combinations/description/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> combine(int n, int k) {
        backtracking(new ArrayList(),n,k,1);
        return result;
    }

    void backtracking(List<Integer> temp,int n,int k,int index){
        if(temp.size() == k){
            result.add(new ArrayList(temp));
            return;
        }
        for(int i = index;i < n + 1;i++){
            temp.add(i);
            backtracking(temp,n,k,i + 1);
            temp.remove(temp.size() - 1);
        }
    }  
}
```
## [Medium] 216. Combination Sum III
**Link** : https://leetcode.com/problems/combination-sum-iii/description/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> combinationSum3(int k, int n) {
        boolean[] used = new boolean[k+1];
        backtracking(k,n,0,new ArrayList(),1);
        return result;

    }
    void backtracking(int k,int n,int sum,List<Integer> temp,int index){
        if(temp.size() == k && sum == n){
            result.add(new ArrayList(temp));
            return;
        }

        for(int i = index; i <= 9;i++){
            temp.add(i);
            sum = sum + i;
            backtracking(k,n,sum,temp,i + 1);
            temp.remove(temp.size() - 1);
            sum = sum - i;
        }
    } 
} 
```
### [Medium] 17. Letter Combinations of a Phone Number
**Link** : https://leetcode.com/problems/letter-combinations-of-a-phone-number/description/
```
class Solution {
    static Map<Character, String> map = new HashMap() {
        {
            put('0', "");
            put('1', "");
            put('2', "abc");
            put('3', "def");
            put('4', "ghi");
            put('5', "jkl");
            put('6', "mno");
            put('7', "pqrs");
            put('8', "tuv");
            put('9', "wxyz");
        }
    };

    List<String> result = new ArrayList();

    public List<String> letterCombinations(String digits) {
        if(digits.length() == 0){
            return result;
        }
        backtracking(digits,new StringBuilder(),0);
        return result;    
    }

    void backtracking(String digits,StringBuilder sb,int index){
        if(index == digits.length()){
            result.add(sb.toString());
            return;
        }
        

        
        String temp = map.get(digits.charAt(index));
        for(char c : temp.toCharArray()){
            sb.append(c);
            backtracking(digits,sb,index + 1);
            sb.deleteCharAt(sb.length() - 1);
        }
    }
}
```
## [Medium]39. Combination Sum
**Link** : https://leetcode.com/problems/combination-sum/description/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> combinationSum(int[] candidates, int target) {
        if(candidates.length == 0){
            return result;
        }
        Arrays.sort(candidates);
        backtracking(candidates,target,0,new ArrayList(),0);
        return result;
    }

    void backtracking(int[] candidates,int target,int sum,List<Integer> current,int index){
        if(sum == target){
            result.add(new ArrayList(current));
        }else if(sum > target){
            return;
        }

        for(int i = index;i < candidates.length;i++){
            if(sum + candidates[i] > target){
                break;
            }
            sum = sum + candidates[i];
            
            current.add(candidates[i]);
            backtracking(candidates,target,sum,current,i);
            sum = sum - candidates[i];
            current.remove(current.size() - 1);
        }
    }
}
```
