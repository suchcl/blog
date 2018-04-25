#### nodejs中的exports和module.exports的区别

这里说到nodejs中的exports和module.exports的区别，应该主要是从ES6中的export串起来的。在使用了ES6的export后想起来node中也有类似的模块技术，这里就简要汇总一下。先说node中的exports和module.exports。

#### node.js中的模块

nodejs的模块其实也很好理解。nodejs中，模块是组成nodejs程序的基本组成部分，文件和模块是一一对应的。简单的理解，就是一个js文件就是一个模块，这个模块可以是js代码，可以是json，也可以是编译过的C或者C++扩展。
每一个node模块执行的时候，即每个node.js的执行文件执行的时候，都会创建一个module对象，同时module对象会创建一个exports属性，该属性的初始化值为{},即一个空对象。

```javascript
module.exports = {};
```

