看下面的代码：

```html
<button class="btn" id="btn">提交</button>
```

```Javascript
btn.onclick = function(){
    function fn(){
        console.log(this);
    }
    fn();
}
```

这样代码执行的结果？不难理解，this指向的是window。这是js作用域的原因。但我们这里的理想的结果并不是想要window，而是想得到btn，怎么处理呢？相信我们大部分人都会声明一个变量来存放btn这个元素，具体代码如下：

```javascript
    btn.onclick = function(){
        var _this = this;
        function fn(){
            console.log(_this);
        }
        fn();  //<button class="btn" id="btn">提交</button>
    }
```
是，这是一个既简单又容易理解的解决方案。
这种场景，有另外的解决方案可以来实现同样的效果，这个时候call、apply、bind就派上用场了。

我们先换一种方式实现上面的this指向的问题，让this指向btn。

```javascript
btn.onclick = function(){
    function fn(){
        console.log(this);
    }
    fn.call(this);  //<button class="btn" id="btn">提交</button>
}
```
由代码的执行结果，我们可以看到没有使用额外变量也让this指向了btn。方法call参数传递进去了一个对象，并且这个对象是要借用的对象。