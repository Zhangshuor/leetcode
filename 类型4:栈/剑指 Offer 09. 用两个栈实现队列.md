
## 类型：栈
## 题目：

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 `appendTail` 和 `deleteHead` ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，`deleteHead` 操作返回 -1 )


### 示例1

```
输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
```
### 示例2
```
输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
```
### 解题思路
实际上只要是入队的操作，我们就将元素压入stack1就可以
出队操作的时候分两种情况：
- 如果stack1,stack2都是空的，那么我们就直接返回-1
- 剩下的情况就是：出队的时候，我们先有一个宏观的思路就是将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素

具体情况如下：
  * 判断stack2是否为空
    + 为空，去判断stack1是否为空，如果stack1不为空，就将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素
    + 不为空，stack2的栈顶元素仍为队首元素，所以下次队列出队的时候可以直接弹出stack2的栈顶元素。
## c++版本

```cpp
class CQueue {
public:
/*实际上只要是入队的操作，我们就将元素压入stack1就可以
出队操作的时候分两种情况：
- 如果stack1,stack2都是空的，那么我们就直接返回-1
- 剩下的情况就是：出队的时候，我们先有一个宏观的思路就是将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素

具体情况如下：
  * 判断stack2是否为空
    + 为空，去判断stack1是否为空，如果stack1不为空，就将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素
    + 不为空，stack2的栈顶元素仍为队首元素，所以下次队列出队的时候可以直接弹出stack2的栈顶元素。*/


    // 定义两个栈
    // stack1用于入栈操作
    // stack2用于出栈操作
    stack<int> stack1;
    stack<int> stack2;
    CQueue() {
    }
// 只要是入队的操作，我们就将元素压入stack1就可以
    void appendTail(int value) {
        stack1.push(value);

    }


    // 在队列头部删除整数：        
    int deleteHead() {
        // 如果stack1和stack2都为空的话，直接返回-1
        if(stack1.empty()&&stack2.empty()) return -1;
        // 判断stack2是否为空
        // 如果stack2为空的话
        if(stack2.empty()){
            // 再判断stack1是否为空，如果不是空的，就将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素（实现在队列头部删除整数的功能）
            while(!stack1.empty()){
                stack2.push(stack1.top());
                stack1.pop();
            }
        }
        // 如果stack2不为空的话
        // stack2的栈顶元素仍为队首元素，所以下次队列出队的时候可以直接弹出stack2的栈顶元素。
        int res = stack2.top();
        stack2.pop();
        return res;
    }
};

/**
 * Your CQueue object will be instantiated and called as such:
 * CQueue* obj = new CQueue();
 * obj->appendTail(value);
 * int param_2 = obj->deleteHead();
 */
```
## python版本

```python
class CQueue:
    '''
实际上只要是入队的操作，我们就将元素压入stack1就可以
出队操作的时候分两种情况：
- 如果stack1,stack2都是空的，那么我们就直接返回-1
- 剩下的情况就是：出队的时候，我们先有一个宏观的思路就是将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素

具体情况如下：
  * 判断stack2是否为空
    + 为空，去判断stack1是否为空，如果stack1不为空，就将stack1里的元素都依次放入stack2，然后由stack2弹出栈顶元素
    + 不为空，stack2的栈顶元素仍为队首元素，所以下次队列出队的时候可以直接弹出stack2的栈顶元素。
    '''

    def __init__(self):
        self.s1,self.s2=[],[]
    
    def appendTail(self, value: int) -> None:
        self.s1.append(value)


    def deleteHead(self) -> int:
        if not self.s1 and not self.s2: return -1
        if not self.s2:
            while self.s1:
                self.s2.append(self.s1.pop())
        return self.s2.pop()



# Your CQueue object will be instantiated and called as such:
# obj = CQueue()
# obj.appendTail(value)
# param_2 = obj.deleteHead()
```
