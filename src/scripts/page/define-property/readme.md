# defineProperty双向绑定
运用了Object.defineProperty来追踪数值的变化和依赖，相当于对数据的读取进行了“劫持”，从而实现双向数据绑定。
## defineProperty使用
>Object.defineProperty() 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性， 并返回这个对象。

使用实例：
    Object.defineProperty(obj, prop, descriptor)

* 参数节
    obj： 要在其上定义属性的对象。
    prop： 要定义或修改的属性的名称。
    descriptor： 将被定义或修改的属性描述符。
* 返回值节
    被传递给函数的对象。

descriptor：对象里目前存在的属性描述符有两种主要形式：`数据描述符`和`存取描述符`。

数据描述符是一个具有值的属性，该值可能是可写的，也可能不是可写的。存取描述符是由getter-setter函数对描述的属性。描述符必须是这两种形式之一；不能同时是两者。

`数据描述符和存取描述符`均具有以下可选键值：
* configurable
    当且仅当该属性的 configurable 为 true 时，该属性描述符才能够被改变，同时该属性也能从对应的对象上被删除。默认为 false。
* enumerable
    当且仅当该属性的enumerable为true时，该属性才能够出现在对象的枚举属性中。默认为 false。

`数据描述符`同时具有以下可选键值：
* value
    该属性对应的值。可以是任何有效的 JavaScript 值（数值，对象，函数等）。默认为 undefined。
* writable
    当且仅当该属性的writable为true时，value才能被赋值运算符改变。默认为 false。

`存取描述符`同时具有以下可选键值：
* get
    一个给属性提供 getter 的方法，如果没有 getter 则为 undefined。当访问该属性时，该方法会被执行，方法执行时没有参数传入，但是会传入this对象（由于继承关系，这里的this并不一定是定义该属性的对象）。
默认为 undefined。
* set
    一个给属性提供 setter 的方法，如果没有 setter 则为 undefined。当属性值修改时，触发执行该方法。该方法将接受唯一参数，即该属性新的参数值。
    默认为 undefined。

## 双向绑定实现

 1. 实现一个数据监听器Observer，能够对数据对象的所有属性进行监听，如有变动可拿到最新值并通知订阅者 
 2. 实现一个指令解析器Compile，对每个元素节点的指令进行扫描和解析，根据指令模板替换数据，以及绑定相应的更新函数 
 3. 实现一个Watcher，作为连接Observer和Compile的桥梁，能够订阅并收到每个属性变动的通知，执行指令绑定的相应回调函数，从而更新视图 
 4. mvvm入口函数，整合以上三者

 ![结构图](https://github.com/DMQ/mvvm/blob/master/img/2.png)


 
 参考：
 1. [160行代码仿Vue实现极简双向绑定-详细注释](http://obkoro1.com/2018/06/24/160%E8%A1%8C%E4%BB%A3%E7%A0%81%E4%BB%BFVue%E5%AE%9E%E7%8E%B0%E6%9E%81%E7%AE%80%E5%8F%8C%E5%90%91%E7%BB%91%E5%AE%9A-%E8%AF%A6%E7%BB%86%E6%B3%A8%E9%87%8A/)
 2. [github上的仿vue双向绑定实现demo](https://github.com/DMQ/mvvm)
