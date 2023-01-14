## 【Medium】LeetCode 24. Swap Nodes in Pairs
**link** : https://leetcode.com/problems/swap-nodes-in-pairs/description/

之前做过的一道题，十分考验对于链表细节的掌握，如果没有处理好很容易产生空指针问题。

**主要思路** : 和很多链表题一样的，由于需要修改头部节点因此先定义一个虚拟头节点，接着将它的指针指向head。接着就是循环的终止条件了，每次循环需要检测当前节点与下个节点是否为空才可以进入循环。
在循环内，定义两个节点first，second，``first = current` `second = current.next`之后将first节点的下一个节点指针指向second的下一位，second的next指针指向first，最后将first的前指针指向next即可完成互换。
最后返回dummy.next

**难点** : 本题如果使用head作为current节点需要记住，head对应的是first节点，first节点发生了改变head也随之改变，因此在更新指针的时候head = head.next而不是head = head.next.next。除此之外，这道题的难点在于判断好终止条件，如果second
在循环外被定义则会造成少循环一次的情况。

**题解** : 

```
class Solution {
    public ListNode swapPairs(ListNode head) {
        ListNode dummyNode = new ListNode(0);
        dummyNode.next = head;
        
        ListNode prev = dummyNode;
        while(head != null && head.next != null){
            ListNode first = head;
            ListNode second = head.next;

            first.next = second.next;
            second.next = first;
            prev.next = second;
            prev = first;
            head = first.next;
            
        }
        return dummyNode.next;
    }
}
```
## 【Medium】 19. Remove Nth Node From End of List
https://leetcode.com/problems/remove-nth-node-from-end-of-list/description/


题目虽然做出来了，但是还是有很多疑问，这道题没有看解题，还没有试过快慢指针的解法

**主要思路** : 首先先遍历一次得到数组的size，之后将size - n获得要删除节点的位置，之后再用一个循环删除节点。

**难点** : 难度不是很大，问题还是出现在头节点的问题上。

**题解** : 

```
class Solution {
    public ListNode removeNthFromEnd(ListNode head, int n) {
        ListNode dummy = new ListNode(0,head);
        ListNode current = head;
        int size = 0;
        while(current != null){
            current = current.next;
            size++;

        }
        ListNode remove = dummy;
        for(int i = 0;i < size - n;i++){
            
            remove = remove.next;
        }
        
        remove.next = remove.next.next;
        return dummy.next;
        
    }
}
```
## 【Easy】 160. Intersection of Two Linked Lists
https://leetcode.com/problems/intersection-of-two-linked-lists/

**题解** : 

```
public class Solution {
    public ListNode getIntersectionNode(ListNode headA, ListNode headB) {
        ListNode currentA = headA;
        ListNode currentB = headB;
        int lenA = 0;
        int lenB = 0;
        while(currentA != null){
            currentA = currentA.next;
            lenA++;
        }

        while(currentB != null){
            currentB = currentB.next;
            lenB++;
        }
        currentA = headA;
        currentB = headB;

        
        if(lenB > lenA){
            int tempLen = lenA;
            lenA = lenB;
            lenB = tempLen;

            ListNode temp = currentA;
            currentA = currentB;
            currentB = temp;
        }

        int gap = lenA - lenB;

        while(gap > 0){
            currentA = currentA.next;
            gap--;
        }

        while(currentA != null){
            if(currentA == currentB){
                return currentA;
            }

            currentA = currentA.next;
            currentB = currentB.next;
        }
        return null;
        
    }
}
```
[Medium] 142. Linked List Cycle II

**题解** : 

```
public class Solution {
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head;
        ListNode fast = head;

        while(fast != null && fast.next != null){
            fast = fast.next.next;
            slow = slow.next;
            if(fast == slow){
                ListNode index1 = head;
                ListNode index2 = fast;
                while(index1 != index2){
                    index1 = index1.next;
                    index2 = index2.next;
                }
                return index1;
            }
        }
        return null;
    }
}
```
