---
layout: default
title: [leetcode(6)]两个数组的交集 II
keywords: leetcode
sitecontent: leetcode
---


两个数组的交集 II
===================

> 给定两个数组，编写一个函数来计算它们的交集。输出结果中每个元素出现的次数，应与元素在两个数组中出现的次数一致。我们可以不考虑输出结果的顺序。

示例：
```javascript
输入: nums1 = [1,2,2,1], nums2 = [2,2]
输出: [2,2]
```

实现：
```javascript
/**
 * @param {number[]} nums1
 * @param {number[]} nums2
 * @return {number[]}
 */
const intersect = function(nums1, nums2) {
    nums1.sort((a,b)=>(a-b));
    nums2.sort((a,b)=>(a-b));
    const len1 = nums1.length,
        len2 = nums2.length;
    const smallArr = len1 < len2 ? nums1 : nums2,
          bigArr = smallArr === nums1 ? nums2 : nums1;
    let resArr = [];
    for (let i = 0; i < smallArr.length; i++) {
        const item = smallArr[i];
        const idx = bigArr.indexOf(item)
        if (idx !== -1) {
            const inter = bigArr.splice(idx, 1);
            resArr = resArr.concat(inter);
        }
    }
    return resArr;
};
```

主要的思路就是，先把两个数组按数字大小进行升序排列，然后，找出长度较小的数组smallArr进行遍历，如果长度大的数组bigArr中包含当前smallArr遍历到的元素，
那么就把这个元素从bigArr中去掉，放入结果数组resArr中，smallArr遍历结束即可得到最终结果。