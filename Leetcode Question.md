
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
