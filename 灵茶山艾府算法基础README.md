### 更适合我的
这里不是说先去啃难题，而是先掌握：

- 数组
  
- 链表
  
- 栈 / 队列
  
- 哈希表
  
- 树的基本概念
  
- 双指针
  
- 二分
  
- 递归
  
- BFS / DFS 的基本思想
  
- 排序的基本认知
  

对客户端岗位来说，前期够用了。  
你不需要一上来就 DP、图论、回溯全精通。

- 哈希表：两数之和
  
- 栈：有效括号
  
- 双指针：移动零、盛最多水的容器
  
- 链表：反转链表、环形链表
  
- 二叉树：最大深度、中序遍历
  
- 二分：二分查找、搜索插入位置
  
- 滑动窗口：长度最小的子数组
  
- BFS / DFS：岛屿数量
  
- 简单 DP：最大子数组和、爬楼梯

## 【0】编程入门

### 数组字符串

[1422. 分割字符串的最大得分](https://leetcode.cn/problems/maximum-score-after-splitting-a-string/)

``` js
/**
 * @param {string} s
 * @return {number}
 */
var maxScore = function(s) {
    let right1 = 0;
    for (const ch of s) {
        if (ch === '1') right1++;
    }

    let ans = 0, left0 = 0;
    for (let i = 0; i < s.length - 1; i++) {
        if (s[i] === '0') {
            left0++;
        } else {
            right1--;
        }
        ans = Math.max(ans, left0 + right1);
    }
    return ans;
};
```



### 前序

#### 数学：因数与倍数

[326. 3 的幂](https://leetcode.cn/problems/power-of-three/)

````typescript
思路：是否是3的n次幂，也就是说一个数如果是 3 的幂（比如 3, 9, 27…），就能一直被 3 整除（n % 3 == 0），不断除以 3，最后一定会变成 1。
如果在除的过程中某一步不能被 3 整除，那它一定不是 3 的幂。
最后判断 n == 1 是否成立即可。
function isPowerOfThree(n: number): boolean {
    if(n<=0){
        return false;
    }
    while(n%3==0){//取模等于0的意思就是能够被整除，while表示，成立就往下走，当不成立的时候，就结束循环。这个算法可以让27变9,9变3,3变1，然后在1除3不成立，就结束了循环
        n=n/3
    }
     if(n==1){
        return true
    }else{
        return false
    }
};
````

[263. 丑数](https://leetcode.cn/problems/ugly-number/)

````typescript
这个还是没太懂，数学底子太差了
function isUgly(n: number): boolean {
    if(n<=0){
        return false
    }
    while(n%3==0){
        n=n/3
    }
    while(n%5==0){
        n=n/5
    }
    return (n&(n-1))===0
};
````



### 相向双指针1

#### [167. 两数之和 II - 输入有序数组](https://leetcode.cn/problems/two-sum-ii-input-array-is-sorted/)

双指针的用法，left+right

```typescript

function twoSum(numbers: number[], target: number): number[] {
    let left=0,right=numbers.length-1 ;/**这个left是第一个下标，right肯定是不能超过这个数组的，如果数组长度是4，那么最后一个数字的下标应该是3，也就是lenth-1**/
    while(true){//这个true不知道是为啥
        let s=numbers[left]+numbers[right]//当时编译没有通过就是因为这个数组我没有加上，直接写的下标，下标的和肯定是不对的，得是数组的左右两个数字的和等于这个s才对
        if(s===target){
            return [left+1,right+1]//正常返回结果值就行了，需要注意的是我们遍历的数组下标都是从0开始的，所以需要加1
        }
        s>target?right--:left++//左右两数加起来是否大于目标值，如果是，那么右边的指针向左移动一位（使其值变小），如果左右两数加起来小于目标值，就让左边的指针向右移动一位（使其值变大）
    }
};
```

#### [15. 三数之和](https://leetcode.cn/problems/3sum/)[还是不太会，第一遍就没懂]

首先需要知道三元组是啥，三元组的def：一个乱的数组，调出三个数字出来（数组长度为3），下标不能重复，这个数组相加的值必须等于0，这就是三元组

```typescript
var threeSum = function(nums) {
    nums.sort((a, b) => a - b);
    const n = nums.length;
    const ans = [];
    for (let i = 0; i < n - 2; i++) {
        const x = nums[i];
        if (i > 0 && x === nums[i - 1]) continue; // 跳过重复数字
        if (x + nums[i + 1] + nums[i + 2] > 0) break; // 优化一
        if (x + nums[n - 2] + nums[n - 1] < 0) continue; // 优化二
        let j = i + 1, k = n - 1;
        while (j < k) {
            const s = x + nums[j] + nums[k];
            if (s > 0) {
                k--;
            } else if (s < 0) {
                j++;
            } else { // 三数之和为 0
                ans.push([x, nums[j], nums[k]]);
                for (j++; j < k && nums[j] === nums[j - 1]; j++); // 跳过重复数字
                for (k--; k > j && nums[k] === nums[k + 1]; k--); // 跳过重复数字
            }
        }
    }
    return ans;
};

```



### 相向双指针2

 



测试更新

再次测试更新222333----测试soucetree



## 自己第一遍遍历hot100

### 技巧

#### [136. 只出现一次的数字](https://leetcode.cn/problems/single-number/)

`^` 是 **按位异或** 运算符。例如：

0 ^ 0 = 0
0 ^ 1 = 1
1 ^ 0 = 1
1 ^ 1 = 0



``` javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var singleNumber = function(nums) {
    let a=0;
    for(const b of nums){
        a^=b//a=a^b
    }
    return a
};
```

#### [169. 多数元素](https://leetcode.cn/problems/majority-element/)

【不是很懂】和上一个题目相反

``` javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var majorityElement = function(nums) {
    let ans=0,hp=0;
    for(const x of nums){
       if(hp===0){
        ans=x;
        hp=1;
       }else{
        hp+=x===ans?1:-1
    }
    }
    return ans
};
```

这里的缩写是：

``` javascript
if (x === ans) {
    hp += 1;
} else {
    hp -= 1;
}
```

也就是：如果当前数字 `x` 和候选人 `ans` 一样，`hp` 加 1

如果不一样，`hp` 减 1

#### [75. 颜色分类](https://leetcode.cn/problems/sort-colors/)

【不是很懂】

``` javascript
/**
 * @param {number[]} nums
 * @return {void} Do not return anything, modify nums in-place instead.
 */
var sortColors = function(nums) {
    let p0=0,p1=0;
    for(let i=0;i<nums.length;i++){
        const x=nums[i]
        nums[i]=2
        if(x<=1){
            nums[p1++]=1
        }
        if(x===0){
            nums[p0++]=0
        }
    }
};
```

#### [31. 下一个排列](https://leetcode.cn/problems/next-permutation/)

【看不懂】
[[31]]



### 双指针

#### [15. 三数之和](https://leetcode.cn/problems/3sum/)

【看不懂，照着答案抄的】首先要知道什么是三元组（三个数相加=0就是三元组）

``` javascript
/**
 * @param {number[]} nums
 * @return {number[][]}
 */
var threeSum = function(nums) {
    nums.sort((a,b)=>(a-b))
    const n=nums.length;
    const ans=[];
    for(let i=0;i<n-2;i++){
            const x=nums[i];
            if(i>0&&x===nums[i-1]) continue;
            if(x+nums[i+1]+nums[i+2]>0)break;
            if(x+nums[n-2]+nums[n-1]<0)continue;
            let j=i+1,k=n-1;
            while(j<k){
                const s=x+nums[j]+nums[k];
                if(s>0){
                    k--;
                }else if(s<0){
                    j++
                }else{
                    ans.push([x,nums[j],nums[k]])
                    for(j++;j<k&&nums[j]===nums[j-1];j++);
                    for(k--;k>j&&nums[k]===nums[k+1];k--);
                }
            }
    }
    return ans
};
```

### 滑动窗口

#### [3. 无重复字符的最长子串](https://leetcode.cn/problems/longest-substring-without-repeating-characters/)

``` javascript
/**
 * @param {string} s
 * @return {number}
 */
var lengthOfLongestSubstring = function(s) {
    let ans=0;//ans结果
    let left=0;//左边的窗口
    const cnt=new Map();//cnt是什么？，开始窗口了，下标left到下标right
    for (let right = 0; right < s.length; right++) {
        const c = s[right];
        cnt.set(c,(cnt.get(c)??0)+1);//这里两个问号是什么，这一句我都不懂
        while (cnt.get(c)>1) {//为什么要这样，这个cnt.get是啥
            cnt.set(s[left],cnt.get(s[left])-1);
            left++;//缩小窗口
            
        }
        ans=Math.max(ans,right-left+1);//更新窗口长度最大值
    }
    return ans
};
```



#### [438. 找到字符串中所有字母异位词](https://leetcode.cn/problems/find-all-anagrams-in-a-string/)

[看不懂这个]

``` javascript
/**
 * @param {string} s
 * @param {string} p
 * @return {number[]}
 */
var findAnagrams = function(s, p) {//s，p是啥
    //统计p的每种字母的出现次数
    const cntp=new Array(26).fill(0)//为社么是26,为什么fill0
    for(const c of p){//c是什么
        cntp[c.charCodeAt()-'a'.charCodeAt()]++//这一行全部看不懂
    }

    const ans=[]
    const cntS=new Array(26).fill(0)//统计s的长为len（p）的子串t的每种字母
    for(let right=0;right<s.length;right++){
        cntS[s[right].charCodeAt()-'a'.charCodeAt()]++//右端点字母进入窗口
        const left=right-p.length+1
        if(left<0){//窗口长度不足
            continue;
        }
        if(_.isEqual(cntS,cntp)){//t和p的每种字母的出现次数都相同
            ans.push(left)//t左边下标



        }
        cntS[s[left].charCodeAt()-'a'.charCodeAt()]--;

    }
    return ans;
    
};
```



### 链表

【看不懂】

#### 反转

``` javascript
/**
 * Definition for singly-linked list.
 * function ListNode(val, next) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.next = (next===undefined ? null : next)
 * }
 */
/**
 * @param {ListNode} head
 * @return {ListNode}
 */
var reverseList = function(head) {
    let pre =null, cur=head;

    while(cur){
        const nxt=cur.next;
        cur.next=pre;
        pre=cur;
        cur=nxt;

    }
    return pre;
};
```

### 数组

#### 53. 最大子数组和

``` javascript
/**
 * @param {number[]} nums
 * @return {number}
 */
var maxSubArray = function (nums) {
    let maxSum = -Infinity//最大和...这个infinity是个啥
    for (let i = 0; i < nums.length; i++) {
        let currentSum = 0//定义当前最大和
        for (let j = i; j < nums.length; j++) {
            currentSum=currentSum+nums[j]//从i累加到j
            //currentSum+=nums[j]，是不是就等于currentSum=nums[j]+1
            maxSum=Math.max(maxSum,currentSum)//最后math.max  
        }//遍历
    }//遍历
        return maxSum


};


```

啥是动态规划

Kadane算法--看不懂，递归也搞不清楚

### 树

#### [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)

``` javascript
/**
 * Definition for a binary tree node.
 * function TreeNode(val, left, right) {
 *     this.val = (val===undefined ? 0 : val)
 *     this.left = (left===undefined ? null : left)
 *     this.right = (right===undefined ? null : right)
 * }
 */
/**
 * @param {TreeNode} root
 * @return {number}
 */
var diameterOfBinaryTree = function(root) {
    let ans=0;
    function dfs(node){//？node是哪里来的,dfs是什么意思，深度搜索？
            if(node===null){
                return -1;//-1是什么意思
            }
            const lLen=dfs(node.left)+1;//
            const rLen=dfs(node.right)+1;
            ans=Math.max(ans,lLen+rLen);
            return Math.max(lLen,rLen)
    }
    dfs(root)
    return ans;
    //   let ans = 0;//最后
    // function dfs(node) {
    //     if (node === null) {
    //         return -1; // 对于叶子来说，链长就是 -1+1=0
    //     }
    //     const lLen = dfs(node.left) + 1; // 左子树最大链长+1
    //     const rLen = dfs(node.right) + 1; // 右子树最大链长+1
    //     ans = Math.max(ans, lLen + rLen); // 两条链拼成路径
    //     return Math.max(lLen, rLen); // 当前子树最大链长
    // }
    // dfs(root);
    // return ans;

 [543. 二叉树的直径](https://leetcode.cn/problems/diameter-of-binary-tree/)
};
```

#### [102. 二叉树的层序遍历](https://leetcode.cn/problems/binary-tree-level-order-traversal/)







