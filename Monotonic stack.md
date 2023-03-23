## [Medium] 739. Daily Temperatures
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
## [easy] 496. Next Greater Element I
```
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        Deque<Integer> deque = new LinkedList();
        int[] result = new int[nums1.length];
        Map<Integer,Integer> map = new HashMap();
        Arrays.fill(result,-1);
        for(int i = 0;i < nums1.length;i++){
            map.put(nums1[i],i);
        }
        deque.push(0);
        for(int i = 1;i < nums2.length;i++){
            if(nums2[i] <= nums2[deque.peek()]){
                deque.push(i);
            }else{
                while(!deque.isEmpty() && nums2[i] > nums2[deque.peek()]){
                    if(map.containsKey(nums2[deque.peek()])){
                        result[map.get(nums2[deque.peek()])] = nums2[i];
   
                    } 
                    deque.pop();   
                }
                deque.push(i);
            }

        }
        return result;
    }
}
```
