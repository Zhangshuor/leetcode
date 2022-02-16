
# 力扣第933题
## 类型：栈
## 题目：

给定一个只包括 `'('，')'，'{'，'}'，'['，']'` 的字符串 `s` ，判断字符串是否有效。

有效字符串需满足：

 1. 左括号必须用相同类型的右括号闭合。
 2.  左括号必须以正确的顺序闭合。

### 示例1

```
输入：s = "()"
输出：true
```
### 示例2

```
输入：s = "()[]{}"
输出：true
```
### 示例3

```
输入：s = "(]"
输出：false
```
### 示例4

```
输入：s = "([)]"
输出：false
```
### 示例5

```
输入：s = "{[]}"
输出：true
```

### 解题思路
[在b站录了一个视频讲解](https://www.bilibili.com/video/BV1Hq4y187EB?share_source=copy_web)
## c++
1. 首先判断字符串中的括号个数是否为偶数
2. 如果是偶数继续进行判断，如果是奇数直接返回`false`
3. 遍历s中的每一个元素
4. 如果遇到的是左括号，那么就将它入栈；如果遇到的是右括号再进行判断
5. 如果遇到的是右括号判断：此时的栈是不是不为空`并且`栈顶元素是不是能和右括号匹配。如果满足，那么将栈顶存的左括号出栈；如果不满足，直接返回`false`。
6. 直到遍历完成，此时栈如果是空的，那就返回`true`
```cpp
class Solution {
public:
    bool isValid(string s) {
        int n = s.size();
        if( n%2 == 1){
            return false;
        }
        unordered_map<char,char> pairs{
            {')','('},
            {']','['},
            {'}','{'}
        };
        stack<char> stk;
        for (char ch: s){
            if (pairs.count(ch)){
                if(stk.empty()||stk.top() != pairs[ch] ){
                    return false;
                }
                stk.pop();
            }
            else{
                stk.push(ch);
            }
        }
        return stk.empty();
    }
};
```

## python
```python
class Solution:
    def isValid(self, s: str) -> bool:
        if len(s) % 2 == 1:
            return False
        
        pairs = {
            ")": "(",
            "]": "[",
            "}": "{",
        }
        stack = list()
        for ch in s:
            if ch in pairs:
                if not stack or stack[-1] != pairs[ch]:
                    return False
                stack.pop()
            else:
                stack.append(ch)
        
        return not stack
```



