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

这里的代码fn.call(this)，就是让借用的对象this去调用fn这个函数，这里的this，就是btn，那么就会很好的理解fn函数种打印的this是btn了。

根据js的一些特性，代码还有以下的一些组织方式：

```javascript
btn.onclick = function () {
    var fn = function () {
        console.log(this);
    }.call(this);  //<button class="btn" id="btn">提交</button>
}

btn.onclick = function () {
    (function () {
        console.log(this);
    }.call(this)); //<button class="btn" id="btn">提交</button>
};
```

接下来看一个具体的知识点，就是改变this的指向。我知道call、apply、bind都可以修改this的指向，下面就具体分析下这些方法的区别。

```javascript
function fn(a, b, c, d) {
    console.log(a, b, c, d);
}

// call
fn.call(null, 1, 2, 3); //1,2,3,undefined

// apply
fn.apply(null, [1, 2, 3]); //1,2,3,undefined

// bind
fn.bind(null,1,2,3)(6);  //1,2,3,6
```

从实例中可以看到，call和apply、bind的第一个参数都是借用的对象，这是3个方法的共同点，不同点是：call是逐个传递参数，apply是传一个数组参数，这2个方法都比较好理解，
bind有一点不同，因为bind不是直接执行而是将绑定好的this重新返回一个新的函数，我们自己可以决定调用时间。将上面的bind实例换个方式更加直观：

```javascript
var fun = fn.bind(null,1,2,3);
fun(7); //1,2,3,7
```