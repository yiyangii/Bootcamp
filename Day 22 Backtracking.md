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
