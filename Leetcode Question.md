
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
## [Easy] 283. Move Zeroes
```
class Solution {
    public void moveZeroes(int[] nums) {
        int fast = 0;
        int slow = 0;
        for(;fast < nums.length;fast++){
            if(nums[fast] != 0){
                nums[slow] = nums[fast];
                slow++;
            }
        }
        for(;slow < fast;slow++){
            nums[slow] = 0;
        }
        
        
    }
}
```
## 922. Sort Array By Parity II
```
class Solution {
    public int[] sortArrayByParityII(int[] nums) {
        int[] result = new int[nums.length];
        int even = 0;
        int odd = 1;
        for(int i = 0;i < nums.length;i++){
            if(nums[i] % 2 == 0){
                result[even] = nums[i];
                even += 2;
            }else{
                result[odd] = nums[i];
                odd += 2;
            }
        }
        return result;
    }
}
```
## 234. Palindrome Linked List
```
class Solution {
    public boolean isPalindrome(ListNode head) {
        if (head == null && head.next == null) return true;

        ListNode slow = head;
        ListNode fast = head;
        ListNode prev = head;
        while(fast != null && fast.next != null){
            prev = slow;
            slow = slow.next;
            fast = fast.next.next;
            
        }
        prev.next = null;
        ListNode current1 = head;
        ListNode current2 = reverse(slow);
        while(current1 != null){
            if(current1.val != current2.val){
                return false;
            }
            current1 = current1.next;
            current2 = current2.next;
        }
        return true;


    }

    public ListNode reverse(ListNode head){
        
        ListNode prev = null;
        while(head != null){
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```
## 143. Reorder List

```
class Solution {
    public void reorderList(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
        }   
        ListNode right = slow.next;
        slow.next = null;
        right = reverse(right);
        ListNode left = head;
        while(right != null){
            ListNode next = left.next;
            ListNode rightNext = right.next;
            left.next = right;
            right.next = next;

            left = next;
            right = rightNext;
        }
       
    }
    public ListNode reverse(ListNode head){
        ListNode prev = null;
        while(head != null){
            ListNode next = head.next;
            head.next = prev;
            prev = head;
            head = next;
        }
        return prev;
    }
}
```
## 141. Linked List Cycle
```
public class Solution {
    public boolean hasCycle(ListNode head) {
        ListNode fast = head;
        ListNode slow = head;
        while(fast != null && fast.next != null){
            slow = slow.next;
            fast = fast.next.next;
            if(slow == fast){
                return true;
            }
        }
        return false;
    }
}
```
## 205. Isomorphic Strings
```
class Solution {
    public boolean isIsomorphic(String s, String t) {

        Map<Character,Character> map1 = new HashMap();
        Map<Character,Character> map2 = new HashMap();
        for(int i = 0;i < s.length();i++){
            if(!map1.containsKey(s.charAt(i))){
                map1.put(s.charAt(i),t.charAt(i));
            }
            if(!map2.containsKey(t.charAt(i))){
                map2.put(t.charAt(i),s.charAt(i));
            }
            if(map1.get(s.charAt(i)) != t.charAt(i) || map2.get(t.charAt(i)) != s.charAt(i)){
                return false;
            }
        }
        return true;
    }
}
```
## 844. Backspace String Compare
```
class Solution {
    

    public boolean backspaceCompare(String s, String t) {
        
        return build(s).equals(build(t));
        
    }

    public String build(String s){
        Stack<Character> stack  = stack = new Stack();
        for(char c : s.toCharArray()){
            if(c != '#'){
                stack.push(c);
            }else if(!stack.isEmpty()){
                stack.pop();
            }
        }
        return String.valueOf(stack);
    }
}
```
## 57. Insert Interval
```
class Solution {
    public int[][] insert(int[][] intervals, int[] newInterval) {
        List<int[]> result = new ArrayList();
        for(int[] i : intervals){
            if(i[1] < newInterval[0]){
                result.add(i);
            }else if(i[0] > newInterval[1]){
                result.add(newInterval);
                newInterval = i;
            }else{
                newInterval[0] = Math.min(newInterval[0],i[0]);
                newInterval[1] = Math.max(newInterval[1],i[1]);
            }
        }
        result.add(newInterval);
        return result.toArray(new int[result.size()][]);
    }
}
```

