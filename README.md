# 双向绑定的demo
[![blog](https://img.shields.io/badge/build-passed-green.svg)](https://github.com/caoweiju/tc_blog)
[![blog](https://img.shields.io/badge/version-v0.0.1-orange.svg)](https://www.caoweiju.com/)

>本文的代码没有经过babel编译[使用class等es6+]，测试方式是在最新的`chrome`上测试，其他的版本和浏览器可能会运行出错。

所有实现都直接写在了对应的`html`的`script`标签内部，没有经过编码。
````
.
├── README.md
├── html
├── package.json
└── src
    ├── scripts
    │   ├── common
    │   ├── page
    │   │   ├── backbone
    │   │   │   ├── index.html
    │   │   │   └── readme.md
    │   │   ├── define-property
    │   │   │   ├── index.html
    │   │   │   └── readme.md
    │   │   ├── dirty-detection
    │   │   │   └── readme.md
    │   │   └── proxy
    │   │       ├── index.html
    │   │       └── readme.md
    │   └── utils
    └── styles
        └── page
````

## 发布订阅 手动绑定

1. 需要简单的封装实现一个订阅发布类
2. 定义`model`对象，任何属性都是通过`get-set`进行读写
3. 订阅发布实例上分别订阅`view-change[input表单的改变事件，需要修改model]`、`model-change[model改变事件，需要修改UI]`
4. `view-change`的事件发布是听通过监听`input表单`的`input事件`来进行发布的。
5. `model-change`事件发布是通过`model`对象的`set`方法进行设置的。

具体实现内容可以查看`/src/scripts/page/backbone/index.html`里面的`js`源码。

## 脏检测
>众所周知，`Angular`的双向绑定是采用“脏检测”的方式来更新`DOM——Angular`对常用的dom事件、xhr事件进行了封装，触发时会调用$digest cycle。在$digest流程中，Angular将遍历每个数据变量的watcher，比较它的新旧值。当新旧值不同时，触发listener函数，执行相关的操作。


## defineProperty

 1. 实现一个数据监听器`Observer`，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者 
 2. 实现一个指令解析器`Compile`，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数 
 3. 实现一个`Watcher`，作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图 
 4. `mvvm`入口函数，整合以上三者

具体实现内容可以查看`/src/scripts/page/defineProperty/index.html`里面的`js`源码。

## proxy
实现方式基本和`defineProperty`一致，但是`proxy`更具有优势和未来；

`defineProperty`和`proxy`对比优略势：


 1. 实现一个数据监听器Observer，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者 
 2. 实现一个指令解析器Compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数 
 3. 实现一个Watcher，作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图 
 4. mvvm入口函数，整合以上三者

具体实现内容可以查看`/src/scripts/page/proxy/index.html`里面的`js`源码。