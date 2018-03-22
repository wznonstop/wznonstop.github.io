---
layout: default
title: react-redux结合,单一组件发生一个点击事件之后发生了什么
keywords: react, redux
sitecontent: react, redux
---


react-redux结合,单一组件发生一个点击事件之后发生了什么
===================


  1.触发一个点击事件，就是想去触发一个action，而点击事件发生在组件里，组件处于view层，是属于react部分的，但是react没有action这些东西，要去redux里面才有，所以需要 react-redux 库的 connect 方法将 react与redux联系起来，即通过 mapStateToProps 和 mapDispatchToProps 方法，将state(这个state不同于之前react里面的state，这里的state是要在reducer里面进行处理的，是属于redux的state) 和 actions、dispatch函数 全部放到 this.props 里面。

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-17-1.png)

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-17-2.png)

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-17-3.png)

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-17-4.png)

![tree](https://raw.githubusercontent.com/wznonstop/wznonstop.github.io/master/images/2016-03-17-5.png)

  2.点击之后就会触发一个action，action就会说明发生了什么事情，也就是指定了一个type，这时就会到 reducer 里面去，根据 action.type 来决定对state作出怎样的更改。state改变之后，由于开始时已经将state绑定到了this.props上，在react框架中，this.props更新，就会自动刷新，而无需再通过redux的 subscribe 来执行刷新操作。要明确一点，react 是处在 view 层的，而引入 redux 是用来处理数据的。














