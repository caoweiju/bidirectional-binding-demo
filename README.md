# 双向绑定的demo
>本文的代码没有经过babel编译[使用class等es6+]，测试方式是在最新的chrome上测试，其他的版本和浏览器可能会运行出错。

## 发布订阅 手动绑定

1. 需要简单的封装实现一个订阅发布类
2. 定义`model`对象，任何属性都是通过`get-set`进行读写
3. 订阅发布实例上分别订阅`view-change[input表单的改变事件，需要修改model]`、`model-change[model改变事件，需要修改UI]`
4. `view-change`的事件发布是听通过监听`input表单`的`input事件`来进行发布的。
5. `model-change`事件发布是通过`model`对象的`set`方法进行设置的。

具体实现内容可以查看`/src/scripts/page/backbone/index.html`里面的`js`源码。
## 脏检测

## defineProperty

## proxy
