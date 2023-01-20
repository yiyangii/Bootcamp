## 【Easy】LeetCode 704 Binary Search
**link** : https://leetcode.com/problems/remove-linked-list-elements/description/

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
