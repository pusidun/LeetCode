```C++
class CQueue {
public:
    CQueue() {

    }
    
    void appendTail(int value) {
        int val;
        while(!st2.empty()){
            val = st2.top();
            st2.pop();
            st1.push(val);
        }
        st1.push(value);
    }
    
    int deleteHead() {
        if(st1.empty() && st2.empty()){
            return -1;
        }
        int val;
        while(!st1.empty()){
            val = st1.top();
            st1.pop();
            st2.push(val);
        }
        val = st2.top();
        st2.pop();
        return val;
    }
private:
    stack<int> st1;
    stack<int> st2;
};
```
两个栈，原数据装进A，逆序，A再倒到B，顺序。那么，A作为添加数据的栈，B作为数据删除的栈。
