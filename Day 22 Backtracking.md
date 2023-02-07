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
