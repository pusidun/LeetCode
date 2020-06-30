# [剑指 Offer 09. 用两个栈实现队列](https://leetcode-cn.com/problems/yong-liang-ge-zhan-shi-xian-dui-lie-lcof/)



![image-20200630082130748](https://i.loli.net/2020/06/30/aCkIBRlHcjhO9uN.png)

## 思路

把数据在两个栈中分别“折腾”一次，出来的顺序就是队列的顺序。

向stack1中push数据——向队列中添加数据

从stack2中弹出数据——从队列中删除头部数据

## 代码

```java
import java.util.Stack;

class CQueue {
    Stack<Integer> stack1;
    Stack<Integer> stack2;
    public CQueue() {
        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }
    public void appendTail(int value) {
        stack1.push(value);
    }
    public int deleteHead() {
        if(!stack2.isEmpty()){
            return stack2.pop();
        }
        if(!stack1.isEmpty()){
            while(!stack1.isEmpty()){
                int temp = stack1.pop();
                stack2.push(temp);
            }
            return stack2.pop();
        }
        return -1;
    }
}

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue obj = new CQueue();
 * obj.appendTail(value);
 * int param_2 = obj.deleteHead();
 */
```

