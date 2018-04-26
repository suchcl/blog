### 遍历DOM元素并设置相关属性

有下面的DOM结构

```html
    <div class="box" id="box">
        <p class="text">呵呵</p>
        <p>How do you do?</p>
        <p class="text">哈哈</p>
        <p>Hello world!</p>
        <p class="text">呼呼</p>
    </div>
```

接下来我想做的是获取到所有class为text的元素，并将这些元素的文字颜色更改为红色。

我们很容易想到使用jQuery来做，简单的实现代码：

```javascript
let pText = $(".text");
for(let i = 0; i < pText.length; i++){
    pText[i].style.color = "#f20";
}
```

效果实现了，但我们应该很快发现，这里出现了DOM而不是jQuery的方法，pText[i].style.color = "#f20";这是DOM方法的经典的属性设置方法。这里涉及到了另外一个知识点，就是DOM对象和jQuery对象的相互转换：

* jQuery对象转换为DOM对象

jQuery对象是一个数据对象，可以通过[index]的方法将jQuery对象转换为DOM对象,如

```javascript
    $(".box")[0]
```

就将jQuery对象$(".box")转换成了DOM对象$(".box")[0]，对了，$(".box")[0]就是一个DOM对象。然后看我们上面的例子代码：

```javascript
for(let i = 0; i < pText.length; i++){
    pText[i].style.color = "#f20";
}
```

pText[i].style.color = "#f20";这行代码的pText[i]就是将jQuery对象转换成了DOM对象，所以才有了后面的经典的DOM对象属性设置的方式，也就正常了。所以这里的遍历DOM元素的方式，并不能算是真正的jQuery的实现方式，充其量算是一种混合的实现方式吧。

* DOM对象转换为jQuery对象

将DOM对象转换成一个jQuery对象就简单多了，就是将一个DOM对象使用$()包裹起来，就完成了对象又DOM到jQuery身份的转变了。

回到我们的整体，再看一种完全由jQuery方法实现的遍历DOM的方法：

```javascript
let pText = $(".text");
pText.each(function(){
    $(this).css("color","#369");
});
```

这里就毫无疑问了，也不用解释什么了，全部都是jQuery的方法，就是纯粹的jQuery来实现的了。

最后我们看使用原生js的实现：

```javascript
let pText = $(".text");
for(let i = 0; i < pText.length; i++){
    pText[i].style.color = "#f20";
}
```

这种的实现方式和上面jQuery的实现方式相同，纯粹的原生js实现功能，没有借助jQuery以及其他的第三方库。