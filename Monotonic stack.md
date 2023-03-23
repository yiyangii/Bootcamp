## 739. Daily Temperatures
```
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int[] result = new int[temperatures.length];
        Deque<Integer> deque = new LinkedList();
        deque.push(0);
        for(int i = 1; i < temperatures.length;i++){
            if(temperatures[i] <= temperatures[deque.peek()]){
                deque.push(i);
            }else{
                while(!deque.isEmpty() && temperatures[i] > temperatures[deque.peek()]){
                    result[deque.peek()] = i - deque.peek();
                    deque.pop();

                }
                deque.push(i);
            }
        }
        return result;
    }
}
```
