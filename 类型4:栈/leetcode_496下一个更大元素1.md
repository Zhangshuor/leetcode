
# 力扣第206题
## 类型：栈
## 题目：
`nums1` 中数字 `x` 的 `下一个更大元素` 是指 `x` 在 `nums2` 中对应位置 `右侧` 的 `第一个` 比 `x` 大的元素。

给你两个 `没有重复元素` 的数组 `nums1` 和 `nums2` ，下标从 `0` 开始计数，其中`nums1` 是 `nums2` 的子集。

对于每个 `0 <= i < nums1.length` ，找出满足 `nums1[i] == nums2[j]` 的下标 `j` ，并且在 `nums2` 确定 `nums2[j]` 的 `下一个更大元素` 。如果不存在下一个更大元素，那么本次查询的答案是 `-1` 。

返回一个长度为 `nums1.length` 的数组 `ans` 作为答案，满足 `ans[i]` 是如上所述的 下一个更大元素 。

### 示例1

```
输入：nums1 = [4,1,2], nums2 = [1,3,4,2].
输出：[-1,3,-1]
解释：nums1 中每个值的下一个更大元素如下所述：
- 4 ，用加粗斜体标识，nums2 = [1,3,4,2]。不存在下一个更大元素，所以答案是 -1 。
- 1 ，用加粗斜体标识，nums2 = [1,3,4,2]。下一个更大元素是 3 。
- 2 ，用加粗斜体标识，nums2 = [1,3,4,2]。不存在下一个更大元素，所以答案是 -1 。

```
### 示例2
```
输入：head = [1,2]
输出：[2,1]
```
### 解题思路
思路提醒：单调栈+哈希表
详细思路见下图和代码注释

![在这里插入图片描述](https://img-blog.csdnimg.cn/d718b5538bfc4cda81abbb73b380a53c.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAY29kZXJfc3VyZQ==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)
![在这里插入图片描述](https://img-blog.csdnimg.cn/7af0a49739b44da686d9f16216706158.png?x-oss-process=image/watermark,type_d3F5LXplbmhlaQ,shadow_50,text_Q1NETiBAY29kZXJfc3VyZQ==,size_20,color_FFFFFF,t_70,g_se,x_16#pic_center)



## c++版本1 

```cpp
class Solution {
public:
    vector<int> nextGreaterElement(vector<int>& nums1, vector<int>& nums2) {
        stack<int> s;//定义一个栈
        unordered_map<int,int> num_map;//定义一个hashmap
        int size = nums1.size();//nums1的长度，例子1中为3
        vector<int> vec_num;//定义一个最后返回的数组容器
        for(int i = 0;i < nums2.size();++i)//遍历nums2
        {
            while(!s.empty() && nums2[i]>s.top())//栈不是空的并且现在遍历的这个元素大于栈中的元素
            {
                num_map[s.top()] = nums2[i];//这个栈中的元素作为key,现在遍历的这个元素作为value
                s.pop();//栈中的元素出栈
            }
            s.push(nums2[i]);//如果栈是空的或者现在遍历的这个元素小于栈中元素，入栈
        }
        while(!s.empty())//遍历完之后，栈并不是空的，那么在hashmap中栈中元素的key都赋值为-1
        {
            num_map[s.top()] = -1;
            s.pop();
        }
        for(int i = 0;i<size;++i)//遍历一遍nums1
        {
            vec_num.push_back(num_map[nums1[i]]);//在hashmap中nums1可以对应上的元素的value依次push给vec_nums
        }
        return vec_num;
    }
};
```
![请添加图片描述](https://img-blog.csdnimg.cn/d4644935786b472b9b9440cafb91d278.png)

## c++版本2

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        stack = []
        res_dict = {i:-1 for i in nums2}
        for i in nums2:
            while stack and i > stack[-1]:
                small = stack.pop()
                res_dict[small] = i
            stack.append(i)
        res = []
        for j in nums1:
            res.append(res_dict[j])
        return res
```
![请添加图片描述](https://img-blog.csdnimg.cn/7218d7194ed04cf08fd6a0eeafbefb76.png)

## python版本1
```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        stack = []
        num_map = {}
        res = []
        for i in nums2:
            while stack and i > stack[-1]:
                small = stack.pop()
                num_map[small] = i
            stack.append(i)
        while stack:
            num_map[stack[-1]] = -1
            stack.pop()
        for j in nums1:
            res.append(num_map[j])
        return res
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/b4b7b29084fc47d194e3bb23d864870b.png)
## python版本2

```python
class Solution:
    def nextGreaterElement(self, nums1: List[int], nums2: List[int]) -> List[int]:
        stack = []
        res_dict = {i:-1 for i in nums2}
        for i in nums2:
            while stack and i > stack[-1]:
                small = stack.pop()
                res_dict[small] = i
            stack.append(i)
        res = []
        for j in nums1:
            res.append(res_dict[j])
        return res
```

![请添加图片描述](https://img-blog.csdnimg.cn/1b2daf3c36644b0897c9381671d6f337.png)

