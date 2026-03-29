## 数组基础理论
数组是存放在连续内存空间上相同类型数据的集合
特性：1.下标0开始 2.内存地连续
数组的元素不能删只能被覆盖

leetcode 704:二分查找
https://leetcode.cn/problems/binary-search/
这个题的思路是准备两个变量一个叫做left一个叫做right
left最初时候在索引0的位置，right在最后一个位置numsSize-1
然后通过middle，用nums[middle] compare with target
if nums[middle]>target, update right = middle - 1
if nums[middle]<target, update left =  middle + 1
这里我就考虑不周，少搞了一个==其实还有这个操作
loop the process to the end. while(left<=right)
另外需要注意middle的问题如果数字过大可能会溢出，因此采用left+(right-left)/2
1      2     3    5    8    9
left        middle        right


leetcode 27:移除元素
https://leetcode.cn/problems/remove-element/description/
这个题有两种解法，找到不等于val的个数为k，返回不含这几个的
第一种暴力求解双重for循环，我的思路是用for循环，第一层里面有if，
如果遇到了nums[i] ==val,那么就与后面的元素交换，但这个交换肯定是不够的，因此我们需要两层
思路：if(nums[i] == val)
    {
        int temp = nums[i];
        nums[i] = nums[i+1];
        nums[i+1] = temp;
        //  1   3   4  5 (val==3)
        //  1   4   3  5
        //  1   4   5  3
        //  1   4   5    (numsSize--)

    }
for(int i = 0; i < numsSize; i++) {
    if(nums[i] == val) {              // 关键：numsSize-- 和 i-- 必须在 if 里面
        for(int j = i; j < numsSize - 1; j++) {
            nums[j] = nums[j + 1];    // 直接覆盖，不需要交换
        }
        numsSize--;
        i--;  // 重新检查当前位置（因为覆盖过来的数也可能等于val）
    }
}
return numsSize;

// ❌ 我的错误写法：
// for(int i = 0; i < numsSize; i++) {
//     for(int j = i; j < numsSize - 1; j++) {
//         if(nums[j] == val) { ... }
//     }
//     numsSize--;  // 错误：放在了外层循环里，每次都会执行
//     i--;         // 错误：同上
// }
// 错误点：numsSize-- 和 i-- 应该只在找到val时执行，而不是每次外层循环都执行
注意要细心注意边界情况和排序需要更加熟练

第二种是双指针  slow and fast
说到双指针有两种 快慢和首尾
这里我们可以定义一个新数组，用快慢指针去存，首先它们都处于同一位置开始
先快指针fast移动，每次随着fast的移动都会去判断
if(nums[fast]!=val)，如果满足将fast的值给slow,fast++,slow++
如果等于的话fast++，但是slow留在原地

leetcode 977 有序数组的平方
https://leetcode.cn/problems/squares-of-a-sorted-array/description/
这个题也是分暴力方法
暴力方法这里有很多种就不赘述了和上面方法基本一致，另外鄙人排序算法目前掌握的种类不足之后会进行补充

双指针方法-首尾
因为这个题说明了是一个非递减的顺序数组，知识说可能存在负数，但是一旦平方的话很大概率最大数是从最左或者最右得出
因此我们选择int left = 0; int right = numsSize -1;
因此可以这样就是进行while判断，while(left<=right)，结束条件是走到结尾，不可能出现left>right
//因为题目提出了新数组，因此需要申请
int* res = (int*)malloc(numsSize * sizeof(int));
int k = numsSize - 1;
while(left <= right) {
    if(nums[right] * nums[right] > nums[left] * nums[left]) {
        res[k] = nums[right] * nums[right];
        k--;
        right--;
    } else {   // 包含相等的情况，都取左边
        res[k] = nums[left] * nums[left];
        k--;
        left++;
    }
}
return res;

// ❌ 我的错误写法：
// }else{
//     nums[left]*nums[left]>nums[right]*nums[right]{  // 错误：多余的判断语句
//         res[k] = nums[left]*nums[left];
//         ...
//     }
// }
// 错误点：else 已经覆盖了"right平方 <= left平方"的情况，不需要再写条件判断
// 那行 nums[left]*nums[left]>nums[right]*nums[right]{ 是多余的语法错误