---
layout: default
title: [leetcode(2)]买卖股票的最佳时机 II
keywords: leetcode
sitecontent: leetcode
---


买卖股票的最佳时机 II
===================

> 给定一个数组，它的第 i 个元素是一支给定股票第 i 天的价格。
  设计一个算法来计算你所能获取的最大利润。你可以尽可能地完成更多的交易（多次买卖一支股票）。
  注意：你不能同时参与多笔交易（你必须在再次购买前出售掉之前的股票）。

看到题目我眉头一皱，感觉事情并没有那么简单，于是我画了个图：

   ![流程图](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2018-09-04-1.png)
    
依据流程图的逻辑，写了下面这坨代码：

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    var len = prices.length;
    if (len < 2) return 0;
    var fakePrices1 =  prices.concat([]),
        fakePrices2 =  prices.concat([]),
        increaseStr = JSON.stringify(fakePrices1.sort((a,b)=>(a-b))), 
        decreaseStr = JSON.stringify(fakePrices2.sort(()=>(1)));
    if (decreaseStr === JSON.stringify(prices)) {
        return 0;
    } else if (increaseStr === JSON.stringify(prices)) {
        return prices[len-1] - prices[0];
    } else {
        var signArr = [],
            flagArr = [];
        for (var i = 0; i < (len-1); i++) {
            if (prices[i+1] - prices[i] >= 0) {
                signArr.push(1)
            } else {
                signArr.push(-1)
            }
        }
        var signLen = signArr.length;
        for (var j = 0; j < (signLen-1); j++) {
            if (signArr[j+1] * signArr[j] == -1) {
                flagArr.push(j+1)
            }
        }
        var judgeArr = [],
            flagLen = flagArr.length;
        for (var x = 0; x < flagLen; x++) {
            judgeArr[x] = signArr[flagArr[x]];
        }
        if (judgeArr[0] === -1) {
            flagArr.unshift(0)
        }
        if (judgeArr[judgeArr.length-1] === 1) {
            flagArr.push(len-1);
        }
        var plusSum = 0,
            reduceSum = 0;
        for (var y = 0; y < flagArr.length; y++) {
            if (y % 2 === 0) {
                reduceSum += prices[flagArr[y]];
            } else {
                plusSum += prices[flagArr[y]];
            }
        }
        return plusSum - reduceSum;
    }
};
```

花了挺多时间，总算完成了，我正得意洋洋，看到了提交结果，`执行用时：8720 ms`，执行用时分布图表最大值也就600ms，我这已经大的没边了🤦‍♀️。
内心还有些许的不服，又运行了一次，还是好久！于是我点开看了用时50ms的代码，简单到我一下没反应过来：

```javascript
/**
 * @param {number[]} prices
 * @return {number}
 */
var maxProfit = function(prices) {
    let maxProfit = 0
    let curMin = prices[0]
    for(let i = 1; i < prices.length; i++){
        if (prices[i] > curMin) {
            maxProfit += prices[i] - curMin
        }
        curMin = prices[i]
    }
    return maxProfit
};
```
太妙了啊，细想一下和我在流程图里画的思路是一致的，但是实现却非常巧妙，学习了。















