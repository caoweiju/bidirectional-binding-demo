## proxy
* 语法节
    let p = new Proxy(target, handler);
* 参数节
    * target
        用Proxy包装的目标对象（可以是任何类型的对象，包括原生数组，函数，甚至另一个代理）。
    * handler
        一个对象，其属性是当执行一个操作时定义代理的行为的函数。

目前支持一下13中方法【enumerate已被废弃】
````
handler.apply()
handler.construct()
handler.defineProperty()
handler.deleteProperty()
// handler.enumerate()  // 已废弃
handler.get()
handler.getOwnPropertyDescriptor()
handler.getPrototypeOf()
handler.has()
handler.isExtensible()
handler.ownKeys()
handler.preventExtensions()
handler.set()
handler.setPrototypeOf()
````


````
// get
let handler = {
    get: function(target, name){
        return name in target ? target[name] : 37;
    }
};

let p = new Proxy({}, handler);

p.a = 1;
p.b = undefined;

console.log(p.a, p.b);    // 1, undefined

console.log('c' in p, p.c);    // false, 37

// set
let validator = {
  set: function(obj, prop, value) {
    if (prop === 'age') {
      if (!Number.isInteger(value)) {
        throw new TypeError('The age is not an integer');
      }
      if (value > 200) {
        throw new RangeError('The age seems invalid');
      }
    }

    // The default behavior to store the value
    obj[prop] = value;
  }
};

let person = new Proxy({}, validator);

person.age = 100;

console.log(person.age); 
// 100

person.age = 'young'; 
// 抛出异常: Uncaught TypeError: The age is not an integer

person.age = 300; 
// 抛出异常: Uncaught RangeError: The age seems invalid
````

## 实践
