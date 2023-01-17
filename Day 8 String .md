## 【Easy】LeetCode 344. Reverse String

不多说，双指针搞定

**link** : https://leetcode.com/problems/reverse-string/description/

**题解** : 

```
class Solution {
    public void reverseString(char[] s) {
        int l = 0;
        int r = s.length - 1;
        while(l <= r){
            char c = s[r];
            s[r] = s[l];
            s[l] = c;
            l++;
            r--;
        }
        
    }
}
```
## 【Easy】LeetCode 541. Reverse String II

**link** : https://leetcode.com/problems/reverse-string-ii/description/

看上去是easy，其实是medium。

这道题最难的是理解题意，首先它将字符串中每k个数进行一次调转。第一种情况，字符串的长度length > 2k，那么把前k个数调转，剩下的k个数放入StringBuilder。第二种情况，字符串元素数量小于2k，
但是大于k，那么调转前k个，剩下的加入stringBuilder。第三种，元素数量小于2k，也小于k，那么就加入StringBuilder。

因此首先我们需要一个循环，每次循环index缩进2k从而判断是否要进行第一种情况的操作，同时弄两个index: firstK,secondK.如果firstK大于length，代表剩下的数直接反转就行，如果first小于length，但是second大于
length，那么代表需要反转前k个数，最后的放进result里。如果first，second都小于length，那么进行第一种操作。

**题解** : 

```
class Solution {
    public String reverseStr(String s, int k) {
        StringBuilder result = new StringBuilder();
        int start = 0;
        int length = s.length();
        while(start < length){
            StringBuilder temp = new StringBuilder();
            int firstK = start + k > length ? length : start + k;
            int secondK = start + 2 * k > length ? length : start + 2 * k;
            temp.append(s.substring(start,firstK));
            result.append(temp.reverse());
            if(firstK < secondK){
                result.append(s.substring(firstK,secondK));
            }
            start += 2 * k;
        }
        return result.toString();
        
    }
}
```
【East】剑指 Offer 05. 替换空格

北美leetcode没有，先用截图记录。

![image](https://user-images.githubusercontent.com/70305543/213013709-1ec527c6-6628-412e-aa43-5943a1e5bfe7.png)

简单粗暴，定义一个StringBuilder，遍历字符串，如果当前index是空格则忘StringBuilder里加%20，如果不是则加当前char。


```
class Solution {
    public String replaceSpace(String s) {
        
        StringBuilder sb = new StringBuilder();
        for(int i = 0;i < s.length();i++){
            if(s.charAt(i) == ' '){
                sb.append("%20");
            }else{
                sb.append(s.charAt(i));
            }
        }
        return sb.toString();
    }
}
```

