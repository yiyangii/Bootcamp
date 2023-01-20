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
