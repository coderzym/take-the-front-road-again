1. new 的执行过程是什么？可否模拟一下？

    1. 首先创建一个对象。
    2. 将这个对象的原型与 `new` 的对象进行链接。
    3. 执行函数接受返回值。
    4. 判断是否为对象类型，是则返回对象，不是则返回第一步中创建的对象。

    ```js
    function _new(obj, ...args) {
        let o = Object.create(obj.prototype)
        let res = o.apply(null, args)
        return res instanceof Object ? res : o
    }
    ```

2. new 一个构造函数，如果函数返回 return {} 、 return null ， return 1 ， return true 会发生什么情况？

如果返回的是对象，如`{}`，那就会返回`{}`，否则会返回 `new` 这个构造函数的实例。

3. new操作符的this绑定优先级是？

`new`的操作符优先级最高，即使使用`bind`绑定了一个对象，最后`new`出来的实例`this`依然指向`new`的构造函数。