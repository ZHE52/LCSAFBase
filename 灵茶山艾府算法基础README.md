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

#### [15. 三数之和](https://leetcode.cn/problems/3sum/)

首先需要知道三元组是啥，三元组的def：一个乱的数组，调出三个数字出来（数组长度为3），下标不能重复，这个数组相加的值必须等于0，这就是三元组

### 相向双指针2
