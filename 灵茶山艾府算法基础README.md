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

作者：灵茶山艾府
链接：https://leetcode.cn/problems/3sum/solutions/1968332/shuang-zhi-zhen-xiang-bu-ming-bai-yi-ge-pno55/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



### 相向双指针2
