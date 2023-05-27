# 🗡指offer一刷记录

## 剑指1



### 36.后缀表达式

要转化为c风格的字符串：`st.push(atoi(token.c_str()));`

```cpp
class Solution {
public:
    int evalRPN(vector<string>& tokens) {
        stack<int> st;
        for(auto token:tokens){
            if(token == "+" || token == "-" || token == "*" || token == "/"){
                int num1=st.top();
                st.pop();
                int num2=st.top();
                st.pop();
                if(token=="+") st.push(num1+num2);
                else if(token=="-") st.push(num2-num1);
                else if(token=="*") st.push(num2*num1);
                else st.push(num2/num1);
            }
            else{
                st.push(atoi(token.c_str()));
            }
        }
        return st.top();
    }
};
```



### 07.重构二叉树：

```cpp
class Solution {
public:
    TreeNode* buildTree(vector<int>& preorder, vector<int>& inorder) {
        if(preorder.size()==0 || inorder.size()==0) return nullptr;
        TreeNode* head=new TreeNode(preorder[0]);
        if(preorder.size()==1) return head;
        int index=0;
        for(int i=0;i<inorder.size();i++){
            if(inorder[i]==preorder[0]){
                index=i;
            }
        }
        vector<int> leftInorder (inorder.begin(),inorder.begin()+index);
        vector<int> rightInoder (inorder.begin()+index+1,inorder.end());
        vector<int> leftPreoder (preorder.begin()+1,preorder.begin()+1+leftInorder.size());
        vector<int> rightPreoder (preorder.begin()+1+leftInorder.size(),preorder.end());
        head->left = buildTree(leftPreoder,leftInorder);
        head->right = buildTree(rightPreoder,rightInoder);
        return head;
    }
};
```



### ==剑指12.矩阵中的路径（回溯/dfs）==

```cpp
class Solution {
public:
    bool exist(vector<vector<char>>& board, string word) {
        if(board.size()==0 || board[0].size()==0) return word.empty();
        for(int row=0;row<board.size();row++){
            for(int col=0;col<board[0].size();col++){
                if(dfs(board,word,row,col,0)) return true;
            }
        }
        return false;
    }
    bool dfs(vector<vector<char>>& board,const string& word,int row,int col,int index){
        if(index==word.size()) return true;
        if(row<0 || row>=board.size() || col<0 || col>=board[0].size()) return false;
        if(board[row][col]!=word[index]) return false;
        board[row][col]='*';
        if(dfs(board,word,row+1,col,index+1) || dfs(board,word,row-1,col,index+1) || dfs(board,word,row,col+1,index+1) || dfs(board,word,row,col-1,index+1)) return true;
        board[row][col]=word[index];
        return false;
    }
};
```





### 剑指27.二叉树的镜像

```cpp
class Solution {
public:
    TreeNode* mirrorTree(TreeNode* root) {
        if(root==nullptr) return nullptr;
        auto left=root->left;
        auto right=root->right;
        root->left=mirrorTree(right);
        root->right=mirrorTree(left);
        return root;
    }
};
```



### 剑指28.对称的二叉树

```cpp
class Solution {
public:
    bool isSymmetric(TreeNode* root) {
        if(root==nullptr) return true;
        return compareTree(root->left,root->right);
    }
    bool compareTree(TreeNode* left,TreeNode* right){
        if(left==nullptr && right==nullptr) return true;
        else if(left!=nullptr && right==nullptr) return false;
        else if(left==nullptr && right!=nullptr) return false;
        if(left->val != right->val) return false;
        bool outside=compareTree(left->left,right->right);
        bool inside=compareTree(left->right,right->left);
        return outside&&inside;
    }
};
```



### ==剑指40.最小的K个数==

==复习快排==

[剑指 Offer 40. 最小的 k 个数（基于快速排序的数组划分，清晰图解） - 最小的k个数 - 力扣（LeetCode）](https://leetcode.cn/problems/zui-xiao-de-kge-shu-lcof/solution/jian-zhi-offer-40-zui-xiao-de-k-ge-shu-j-9yze/)

可以使用最小堆来解决，但是复杂度任然高

```cpp
class Solution {
public:
    vector<int> getLeastNumbers(vector<int>& arr, int k) {
        priority_queue<int> pq;
        for(auto i : arr){
            pq.push(i);
            if(pq.size()>k) pq.pop();
        }
        vector<int> res(k,0);
        int i=0;
        while(!pq.empty()){
            res[i]=pq.top();
            pq.pop();
            i++;
        }
        return res;
    }
};
```



### 剑指41.数据流中的中位数

如果使用单个优先队列会超时

正确方法：使用两个堆，一个大顶堆一个小顶堆，根据两个堆的堆顶获得中位数：

![img](https://labuladong.github.io/pictures/%E4%B8%AD%E4%BD%8D%E6%95%B0/2.jpeg)

**判断哪个堆比较大，比较大的那个，推入元素之后把堆顶的放到另外一个堆。**

```cpp
class MedianFinder {
public:
    /** initialize your data structure here. */
    priority_queue<int> Minpq;
    priority_queue<int,vector<int>,greater<int>>Maxpq;
    MedianFinder() {
        
    }
    
    void addNum(int num) {
        if(Minpq.size()<=Maxpq.size()) {
            Maxpq.push(num);
            Minpq.push(Maxpq.top());
            Maxpq.pop();
        }
        else {
            Minpq.push(num);
            Maxpq.push(Minpq.top());
            Minpq.pop();
        }

    }
    
    double findMedian() {
        if(Maxpq.size()>Minpq.size()) return Maxpq.top();
        else if(Maxpq.size()<Minpq.size()) return Minpq.top();
        else return (Maxpq.top()+Minpq.top())/2.0;
    }
};
```



### 剑指44.数字序列中某一位数字：

一位数有几个？`1~9` 共 9 * 1 = 9 个。共几位？共 1 * 9 = 9位。

二位数有几个？`10~99` 共 9 * 10 = 90 个。共几位？共 2 * 90 = 180 位。

三位数有几个？`100~999` 共 9 * 100 = 900 个。共几位？共 3 * 900 = 2700 位。

0单独讨论：



- 首先找到这个数字对应的数是几位数，用 `digits` 表示；
- 然后确定这个对应的数的数值 `target`；
- 最后确定返回值是 `target` 中的哪个数字。

![image-20230423163747498](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230423163747498.png)

```cpp
class Solution {
public:
    int findNthDigit(int n) {
        int digit = 1; 
        long start = 1; 
        long count = digit * start * 9; 
        while (n > count) {
            n -= count;
            digit += 1;
            start *= 10;
            count = digit * start * 9;
        }
        
        long number = start + (n - 1) / digit;
       
        string s_number = to_string(number);
        return s_number[(n - 1) % digit] - '0';
    }
};
};
```

**在后面n要减去1；**



### ==剑指51.数组中的逆序对==

==「归并排序」与「逆序对」是息息相关的==。归并排序体现了 “分而治之” 的算法思想

![image-20230507193229046](C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230507193229046.png)

合并阶段 本质上是 合并两个排序数组的过程，**而每当遇到 左子数组当前元素 > 右子数组当前元素 时，意味着 「左子数组当前元素 至 末尾元素」 与 「右子数组当前元素」 构成了若干 「逆序对」 。**

考虑在归并排序的合并阶段统计「逆序对」数量，完成归并排序时，也随之完成所有逆序对的统计。

```cpp
class Solution {
public:
    int reversePairs(vector<int>& nums) {
        vector<int> tmp(nums.size());
        return mergeSort(0, nums.size() - 1, nums, tmp);
    }
private:
    int mergeSort(int l, int r, vector<int>& nums, vector<int>& tmp) {
        // 终止条件
        if (l >= r) return 0;
        // 递归划分
        int m = (l + r) / 2;
        int res = mergeSort(l, m, nums, tmp) + mergeSort(m + 1, r, nums, tmp);
        // 合并阶段
        int i = l, j = m + 1;
        for (int k = l; k <= r; k++)
            tmp[k] = nums[k];
        for (int k = l; k <= r; k++) {
            if (i == m + 1)
                nums[k] = tmp[j++];
            else if (j == r + 1 || tmp[i] <= tmp[j])
                nums[k] = tmp[i++];
            else {
                nums[k] = tmp[j++];
                res += m - i + 1; // 统计逆序对
            }
        }
        return res;
    }
};
```



### 1143.最长公共子序列

dp数组的含义：`dp[i][j]`表示长度为：`[0,i-1]`的字符串text1与长度为【0，j-1】的text2的最长公共子序列长度。

为什么不定义从i或者j开始呢？

**==根据`dp[i][j]`的定义，`dp[i][0] `和`dp[0][j]`其实都是没有意义的！==**

`如果定义 dp[i][j]为 以下标i为结尾的A，和以下标j 为结尾的B，那么 第一行和第一列毕竟要进行初始化，如果nums1[i] 与 nums2[0] 相同的话，对应的 dp[i][0]就要初始为1， 因为此时最长重复子数组为1。 nums2[j] 与 nums1[0]相同的话，同理。`

<img src="C:\Users\gaohan\AppData\Roaming\Typora\typora-user-images\image-20230514111231666.png" alt="image-20230514111231666" style="zoom:50%;" />

```cpp
class Solution {
public:
    int longestCommonSubsequence(string text1, string text2) {
        if(text1.size()==0||text2.size()==0) return 0;
        int res=0;
        vector<vector<int>> dp(text1.size()+1,vector<int>(text2.size()+1,0));
        for(int i=1;i<=text1.size();i++){
            for(int j=1;j<=text2.size();j++){
                if(text1[i-1]==text2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                else{
                    dp[i][j]=max(dp[i-1][j],dp[i][j-1]);
                }
                if(dp[i][j]>res) res=dp[i][j];
            }
        }
        return res;
    }
};
```



### 718.最长重复子数组

==子数组必须是连续的，子序列可以不连续==

连续的话，只要不等就要continue；

```cpp
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>> dp(nums1.size()+1,vector<int>(nums2.size()+1,0));
        int result=0;
        for(int i=1;i<=nums1.size();i++){
            for(int j=1;j<=nums2.size();j++){
                if(nums1[i-1]==nums2[j-1]){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                //else dp[i][j]=0;
                result=max(result,dp[i][j]);
            }
        }
        return result;
    }
};
```



用i，j表示的数组的写法，要初始化初始情况：

```cpp
class Solution {
public:
    int findLength(vector<int>& nums1, vector<int>& nums2) {
        vector<vector<int>> dp(nums1.size(),vector<int>(nums2.size(),0));
        int result=0;
        for(int i=0;i<nums1.size();i++){
            if(nums1[i]==nums2[0]) dp[i][0]=1;
        }
        for(int j=0;j<nums2.size();j++){
            if(nums2[j]==nums1[0]) dp[0][j]=1;
        }
        for(int i=0;i<nums1.size();i++){
            for(int j=0;j<nums2.size();j++){
                if(nums1[i]==nums2[j] && i>0 && j>0){
                    dp[i][j]=dp[i-1][j-1]+1;
                }
                //else dp[i][j]=0;
                result=max(result,dp[i][j]);
            }
        }
        return result;
    }
};
```



### ==剑指Ⅱ.33变位词分组==

明显的哈希，但是哈希表要做成第二个元素是vector<string>的。

```cpp
class Solution {
public:
    vector<vector<string>> groupAnagrams(vector<string>& strs) {
        vector<vector<string>> result;
        unordered_map<string,vector<string>> mp;
        for(auto str:strs){
            auto tmp=str;
            sort(tmp.begin(),tmp.end());
            mp[tmp].push_back(str);
        }
        for(auto it:mp){
            result.push_back(it.second);
        }
        return result;
    }
};
```



### 剑指Ⅱ.34 外星词排序

```cpp
class Solution {
public:
    bool isAlienSorted(vector<string>& words, string order) {
        if(words.size()<=1) return true;
        unordered_map<char,int> mp;
        for(int i=0;i<order.size();i++){
            mp[order[i]]=i;
        }
        for(int i=1;i<words.size();i++){
            if(!compare(words[i-1],words[i],mp)){
                return false;
            }
        }
        return true;
    }
    bool compare(string &s1,string &s2,unordered_map<char,int>& mp){
        int point=0;
        while(point<s1.size() && point<s2.size()){
            if(mp[s1[point]] > mp[s2[point]]){
                return false;
            }
            else if(mp[s1[point]] < mp[s2[point]]){
                return true;
            }
            else point++;
        }
        if(point == s1.size() && point <=s2.size()) return true;
        else return false;
    }
};
```

