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
## [Medium] 40. Combination Sum II
**Link** : https://leetcode.com/problems/combination-sum-ii/description/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    
    public List<List<Integer>> combinationSum2(int[] candidates, int target) {
        Arrays.sort(candidates);
        boolean[] used = new boolean[candidates.length];
        Arrays.fill(used,false);
        backtracking(0,new ArrayList(),candidates,target,0,used);
        return result;
    }

    void backtracking(int sum,List<Integer> current,int[] candidates,int target,int index,boolean[] used){
        if(sum == target){
            result.add(new ArrayList(current));
            return;
        }

        for(int i = index;i < candidates.length;i++){
            if(sum + candidates[i] > target){
                break;
            }
            if(i > 0 && candidates[i - 1] == candidates[i] && !used[i - 1]){
                continue;
            }

            current.add(candidates[i]);
            sum += candidates[i];
            used[i] = true;
            backtracking(sum,current,candidates,target,i + 1,used);
            sum -= candidates[i];
            current.remove(current.size() - 1);
            used[i] = false;
        }
        
    }
}
```
## [Medium] 131. Palindrome Partitioning
**Link** : https://leetcode.com/problems/palindrome-partitioning/description/
```
class Solution {
    public List<List<String>> partition(String s) {
        List<List<String>> result = new ArrayList();

        dfs(0,result,new ArrayList<String>(),s);
        return result;

    }

    public void dfs(int start,List<List<String>> result,List<String> current,String s){
        
        if(start >= s.length()){
            result.add(new ArrayList(current));
        }
        for(int end = start;end < s.length();end++){
            if(checkP(start,end,s)){
                current.add(s.substring(start,end+1));   
                dfs(end+1,result,current,s);
                current.remove(current.size()-1);
            }
        }


    }

    public boolean checkP(int start,int end,String temp){
        while(start < end){
            if(temp.charAt(start) != temp.charAt(end)){
                return false;
            }
            start++;
            end--;
        }
        return true;
    }
}
```
## [Medium] 93. Restore IP Addresses
**Link** : https://leetcode.com/problems/restore-ip-addresses/description/
```
class Solution {
    List<String> result = new ArrayList();
    public List<String> restoreIpAddresses(String s) {
        
        dfs(s,new StringBuilder(),3,0);
        return result;
    }
    void dfs(String s,StringBuilder sb,int dot,int index){
        if(dot == 0){
            if(valid(s.substring(index))){
                sb.append('.' + s.substring(index));
                result.add(sb.toString());
            }
            return;
        }
        for(int i = index;i < s.length();i++){
            if(valid(s.substring(index,i + 1))){
                int length = sb.length();
                if(dot == 3){
                    sb.append(s.substring(index,i + 1));
                    dfs(s,sb,dot-1,i + 1);
                    sb.setLength(length);
                }else{
                    sb.append('.' + s.substring(index,i + 1));
                    dfs(s,sb,dot - 1,i + 1);
                    sb.setLength(length);
                }
            }
        }
    }
    boolean valid(String s){     
        if(s.length() > 3 ){
            return false;
        }
        if(s.length() < 1){
            return false;
        }
        if(s.charAt(0) == '0' && s.length() > 1){
            return false;
        }
        if(Integer.valueOf(s) > 255){
            return false;
        }
        return true;
    }   
}
```
## [Medium] 78. Subsets
**Link** : https://leetcode.com/problems/subsets/description/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
 
    public List<List<Integer>> subsets(int[] nums) {
        
        dfs(0,new ArrayList(),nums,result);
        return result;
        
    }

    public void dfs(int start,List<Integer> current,int[] nums,List<List<Integer>> result){
        result.add(new ArrayList(current));
        if(start >= nums.length){
            return;
        }

        for(int i = start;i < nums.length;i++){
            current.add(nums[i]);
            dfs(i + 1,current,nums,result);
            current.remove(current.size() - 1);
        }
    }
}
```
## [Medium] 90. Subsets II
**Link** : https://leetcode.com/problems/subsets-ii/
```
class Solution {
    public List<List<Integer>> subsetsWithDup(int[] nums) {
        Arrays.sort(nums);
        List<List<Integer>> result = new ArrayList();
        dfs(0,new ArrayList(),nums,result);
        return result;
    }

    public void dfs(int start,List<Integer> current,int[] nums,List<List<Integer>> result){
        result.add(new ArrayList(current));
        for(int i = start;i < nums.length;i++){
            if(i != start && nums[i] == nums[i - 1]){
                continue;
            }
            current.add(nums[i]);
            dfs(i + 1,current,nums,result);
            current.remove(current.size() - 1);
        }
    }

    
}
```
## [Medium] 491. Non-decreasing Subsequences
**Link** : https://leetcode.com/problems/non-decreasing-subsequences/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> findSubsequences(int[] nums) {
        dfs(nums,0,new ArrayList());
        return result;
    }
    void dfs(int[] nums,int index,List<Integer> current){
        if(current.size() > 1){
            result.add(new ArrayList(current));
       
        }
        int[] used = new int[201];

        for(int i = index;i < nums.length;i++){
            if(!current.isEmpty() && current.get(current.size() - 1) > nums[i] 
            || used[nums[i]+100] == 1){
                continue;
            }
            
            current.add(nums[i]);
            used[nums[i] + 100] = 1;
            dfs(nums,i + 1,current);
            current.remove(current.size()-1);
        }

    }
}
```

## [Medium] 46. Permutations
**Link** : https://leetcode.com/problems/permutations/
```
class Solution {
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<List<Integer>>();
        List<Integer> temp = new ArrayList<Integer>();
        dfs(result,nums.length,nums,temp);
        
        return result;
        
    }
    public void dfs(List<List<Integer>> result,int length,int[] nums,List<Integer> temp){
       
        
        if(temp.size() == length){
            result.add(new ArrayList<Integer>(temp));   
        }else{
            for(int i = 0;i < length;i++){
                if(temp.contains(nums[i])){
                    continue;
                }
                temp.add(nums[i]);
                dfs(result,length,nums,temp);
                temp.remove(temp.size() - 1);
            }
        }
        
    }
}
```
##[Medium] 47. Permutations II
**Link** : https://leetcode.com/problems/permutations-ii/submissions/895701746/
```
class Solution {
    List<List<Integer>> result = new ArrayList();
    public List<List<Integer>> permuteUnique(int[] nums) {
        Arrays.sort(nums);
        if(nums.length == 0 || nums == null){
            return result;
        }
        boolean[] used = new boolean[nums.length];
        backtracking(nums,new ArrayList(),0,used);
        return result;
    }

    void backtracking(int[] nums,List<Integer> current,int index,boolean[] used){
        if(current.size() == nums.length){
            result.add(new ArrayList(current));
            return;
        }
        
        for(int i = 0;i < nums.length;i++){
            if(used[i] == true){
                continue;
            }
            if(i > 0 && nums[i] == nums[i - 1] && used[i - 1] == true){
                continue;
            }
            current.add(nums[i]);
            used[i] = true;
            backtracking(nums,current,i,used);
            current.remove(current.size() - 1);
            used[i] = false;

        }
    }
}
```
## [Hard]332. Reconstruct Itinerary
**Link** : https://leetcode.com/problems/reconstruct-itinerary/description/
```
class Solution {
    LinkedList<String> current = new LinkedList();
    LinkedList<String> result;
    public List<String> findItinerary(List<List<String>> tickets) {
        Collections.sort(tickets, (a, b) -> a.get(1).compareTo(b.get(1)));
        boolean[] used = new boolean[tickets.size()];
        current.add("JFK");
        backtracking((ArrayList)tickets,used);
        return result;

    }

    public boolean backtracking(ArrayList<List<String>> tickets,boolean[] used){
        if(current.size() == tickets.size() + 1){
            result = new LinkedList(current);
            return true;
        }

        for(int i = 0;i < tickets.size();i++){
            if(!used[i] && tickets.get(i).get(0).equals(current.getLast())){
                current.add(tickets.get(i).get(1));
                used[i] = true;
                if(backtracking(tickets,used)){
                    return true;
                }
                used[i] = false;
                current.removeLast();
            }
        }
        return false;
    }
}
```
## [Hard] 51. N-Queens
**Link** : https://leetcode.com/problems/n-queens/
```
class Solution {
    List<List<String>> result = new ArrayList();
    public List<List<String>> solveNQueens(int n) {
        char[][] board = new char[n][n];
        for(char[] c : board){
            Arrays.fill(c,'.');
        }
        dfs(board,0,n);
        return result;
        
    }

    void dfs(char[][] board,int index,int n){
        if(index == n){
            result.add(toList(board));
            return;
        }

        for(int i = 0;i < n;i++){
            if(isVlid(index,i,board,n)){
                board[index][i] = 'Q';
                dfs(board,index + 1,n);
                board[index][i] = '.';
            }
        }
    }

    boolean isVlid(int x,int y,char[][] board,int n){
        for(int i = 0;i < n;i++){
            if(board[x][i] == 'Q'){
                return false;
            }
        }

        for(int j = 0;j < n;j++){
            if(board[j][y] == 'Q'){
                return false;
            }
        }

        for(int i = 0;i < n;i++){
            if(x + i < board.length && y + i < board.length){
                if(board[x+i][y+i] == 'Q'){
                    return false;
                }
            }
        }

        for(int i = 0;i < n;i++){
            if(x + i < board.length && y - i >= 0){
                if(board[x+i][y-i] == 'Q'){
                    return false;
                }
            }
        }

        for(int i = 0;i < n;i++){
            if(x - i >= 0 && y + i < board.length){
                if(board[x-i][y+i] == 'Q'){
                    return false;
                }
            }
        }

        for(int i = 0;i < n;i++){
            if(x - i >= 0 && y - i >= 0){
                if(board[x-i][y-i] == 'Q'){
                    return false;
                }
            }
        }

        return true;


    }

    public List toList(char[][] board){
        List<String> ls = new ArrayList();
        for(char[] c : board){
            ls.add(String.copyValueOf(c));
        }
        return ls;
    }
}
```
