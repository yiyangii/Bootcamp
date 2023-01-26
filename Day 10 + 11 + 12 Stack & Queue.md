## 【Easy】LeetCode 232. Implement Queue using Stacks
**link** : https://leetcode.com/problems/implement-queue-using-stacks/

```
class MyQueue {
    Stack<Integer> in = new Stack();
    Stack<Integer> out = new Stack();
    public MyQueue() {
        
    }
    
    public void push(int x) {
        in.push(x);
    }
    
    public int pop() {
        dump();
        return out.pop();
    }
    
    public int peek() {
        dump();
        return out.peek();
    }
    
    public boolean empty() {
        return in.isEmpty() && out.isEmpty();
    }

    public void dump(){
        if(!out.isEmpty()){
            return;
        }

        while(!in.isEmpty()){
            out.push(in.pop());
        }
    }
}
```

## 【Easy】LeetCode 225. Implement Stack using Queues
**link** : https://leetcode.com/problems/implement-stack-using-queues/description/


```
class MyStack {
    Queue<Integer> queue = new LinkedList();
    Queue<Integer> temp = new LinkedList();
    public MyStack() {
        queue =  new LinkedList();
        temp = new LinkedList();
    }
    
    public void push(int x) {
        temp.offer(x);
        while(!queue.isEmpty()){
            temp.offer(queue.poll());
        }
        Queue<Integer> buffer = new LinkedList();
        buffer = temp;
        temp = queue;
        queue = buffer;
    }
    
    public int pop() {
        return queue.poll();
    }
    
    public int top() {
        return queue.peek();
    }
    
    public boolean empty() {
        return queue.isEmpty();
    }
}

```

## 【Easy】LeetCode 20. Valid Parentheses
**link** : https://leetcode.com/problems/valid-parentheses/description/

```
class Solution {
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<Character>();
        for(char c : s.toCharArray()){
            if(c == '('){
                stack.push(')');
            }else if(c == '['){
                stack.push(']');
            }else if(c == '{'){
                stack.push('}');
            }else if(stack.isEmpty() || stack.pop() != c){
                return false;
            }
        }
        return stack.isEmpty();
                
         
    }
}
```

## [Easy] Leetcode 1047. Remove All Adjacent Duplicates In String
**link** : https://leetcode.com/problems/remove-all-adjacent-duplicates-in-string/description/

```
class Solution {
    public String removeDuplicates(String s) {
        Stack<Character> stack = new Stack();
        String result = "";
        for(char c : s.toCharArray()){
            if(stack.isEmpty() || stack.peek() != c){
                stack.push(c);
            }else{
                stack.pop();
            }
        }

        while(!stack.isEmpty()){
            result = stack.pop() + result;
        }
        return result;
    }
```
## [Medium] Leetcode 150. Evaluate Reverse Polish Notation
**link** : https://leetcode.com/problems/evaluate-reverse-polish-notation/description/

```
class Solution {
    public int evalRPN(String[] tokens) {
        Stack<Integer> stack = new Stack();
        for(String s : tokens){
            if("+".equals(s)){
                stack.push(stack.pop() + stack.pop());
            }else if("-".equals(s)){
                stack.push(-stack.pop() + stack.pop());
            }else if("*".equals(s)){
                stack.push(stack.pop() * stack.pop());
            }else if("/".equals(s)){
                int temp1 = stack.pop();
                int temp2 = stack.pop();
                stack.push(temp2 / temp1);
            }else{
                stack.push(Integer.valueOf(s));
            }
        }
        return stack.pop();
    }
}
```
## [Hard] Leetcode 239. Sliding Window Maximum
**link** : https://leetcode.com/problems/sliding-window-maximum/description/

```
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {

        if(nums.length == 1){
            return nums;
        }
        myQueue queue = new myQueue();
        int[] result = new int[nums.length - k + 1];
        int index = 0;
        for(int i = 0;i < k;i++){
             queue.add(nums[i]);
        }
        result[index] = queue.peek();
        index++;
        for(int i = k;i < nums.length;i++){
            queue.poll(nums[i - k]);
            queue.add(nums[i]);
            
            result[index] = queue.peek();
            index++;
        }
        return result;


    }

    
}
class myQueue{
       Deque<Integer> deque = new LinkedList<>(); 

       void poll(int val){
           if(!deque.isEmpty() && val == deque.peek()){
               deque.poll();
           }
       }

       void add(int val){
           while(!deque.isEmpty() &&  val > deque.getLast()){
               deque.removeLast();
           }
           deque.add(val);
       }

       int peek(){
           return deque.peek();
       }


}
```

