## 【Easy】LeetCode 704 Binary Search
**link** : https://leetcode.com/problems/remove-linked-list-elements/description/

一道基础的链表题，主要考察的是对链表头节点的理解以及它如何删除元素

**主要思路** ：由于链表中移除元素都依靠前一位节点，因此需要考虑头节点的处理。可以先创建一个dummy节点并且让它与头节点相连 `dummy.next = head`，
之后创建一个prev节点用于存储遍历过程中节点的前一位，一个current节点用于遍历整个链表，当`current.val = val`的时候通过`prev.next = current.next`来完成移除操作，最后更新prev与current节点。
值得注意的是，由于已经遍历了整个链表，因为返回值不应该为current或者prev的任何一个，因为它们已经是链表的最后一位与倒数第二位，在这里需要返回的是dummy.next也就是整个链表的头节点。

**难点** ： 了解处理头部节点，学习移除元素的操作与链表处理。

**题解**：

```
class Solution {
    public ListNode removeElements(ListNode head, int val) {
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        ListNode current = head;
        while(current != null){
            if(current.val == val){
                prev.next = current.next;
            }else{
                prev = current;
            }
            current = current.next;
        }
        return dummy.next;
    }
}
```
## 【Medium】707. Design Linked List

一道题搞定理解所有链表操作

**主要思路** : 这道题考的是对链表的掌握度，如果掌握了链表的关键信息，解题就十分简单了。

**题解**：

```
class ListNode{
    ListNode next;
    int val;
    ListNode(){}
    ListNode(int val){
        this.val = val;
    }

    
}

class MyLinkedList {
    ListNode head;
    int size;
    

    public MyLinkedList() {
        head = new ListNode();
        size = 0;
    }
    
    public int get(int index) {
        if(index >= size || index < 0){
            return -1;
        }
        ListNode temp = head;
        for(int i = 0;i <= index;i++){
            temp = temp.next;
        }
        return temp.val;
        
    }
    
    public void addAtHead(int val) {
        addAtIndex(0,val);
    }
    
    public void addAtTail(int val) {
        addAtIndex(size,val);
    }
    
    public void addAtIndex(int index, int val) {
        if(index > size){
            return;
        }
        if(index < 0){
            index = 0;
        }
        size++;
        ListNode prev = head;
        for(int i = 0;i < index;i++){
            prev = prev.next;
        }

        ListNode add = new ListNode(val);
        ListNode next = prev.next;
        prev.next = add;
        add.next = next;
    }
    
    public void deleteAtIndex(int index) {
        if(index < 0 || index >= size){
            return;
        }
        size--;
        if(index == 0){
            head = head.next;
            return;
        }

        ListNode prev = head;
        for(int i = 0;i < index;i++){
            prev = prev.next;
        }
        prev.next = prev.next.next;
    }
}
```

