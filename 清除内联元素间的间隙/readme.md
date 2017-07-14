### 内联元素之间的间隙

#### 现象

内联元素，设置display:inline;或display:inline-block;的块状元素之间，有一定的间距，但这个间距，并不是我们布局中的效果。

![](images/img1.png)

如图所示，两个按钮之间，以及两个设置了display:inline-block;的块状元素之间，都有一个定间距的间隙，但是这部分间距并不是我们需要的布局效果。

#### 原因

内联元素之间，或者是设置了display:inline;或者display:inline-block;的块状元素之间，这些元素都会默认按照水平方式排列布局，那么这里的间隙就是元素之间的空格造成的。

### 解决

> 设置了display:inline;或者display:inline-block;的块状元素，已经具有了内联元素水平布局的特性，为了方便描述，下面我们暂且称这样的块状元素为内联元素。

上面的原因部分告诉我们这些间距的产生原因是元素之间的空格，那么只要消除了这些标记之间的空格，那么这些间隙自然也就消失了。遵循这样的原则，有一下几种方法可以消除内联元素之间的间隙：

1. 将内联标记写在一行

这中解决方式简单易懂，没有任何技术难度,效果也完美。

```html
<div class="btn-wrap">
    <button class="btn btn-reset">重置</button><button class="btn btn-commit">提交</button>
</div>

<div class="box">
    <div class="b1">b1</div><div class="b2">b2</div>
</div>
```

![](images/img2.png)

但这样人为的将元素写在一行，对于使用集成IDE如WebStorm等的用户，经常代码格式化，或者对代码格式要求严格的同学来说，认为很多写在同一行的代码组织混乱，不易于维护的，会强制格式化代码为分行显示，那么问题就又出来了，所以这种解决方式能满足要求，但不完美。

2. 使用注释

既然元素之间的间隙是由于元素之间的空格产生的，那么我在两个元素之间添加一个注释，注释的内容不会在页面中显示出来，同时也解决了元素之间的空格问题。

```html
<div class="btn-wrap">
    <button class="btn btn-reset">重置</button><!--
    --><button class="btn btn-commit">提交</button>
</div>

<div class="box">
    <div class="b1">b1</div><!--
    --><div class="b2">b2</div>
</div>
```

这种解决方式，把代码分开在两行显示，但是添加了没有意义的注释，仍然不觉着是一种完美的解决方案。

3. 使用margin负值

margin负值的值，是和文字的字号和字体有关系的，不同的字号、字体，已经在不同的浏览器上面，letter-spacing值是不同的，所以这种方法如果就改某个特定场景下的问题是可以的，但不适合大规模使用。

4. 标签不闭合

我们的要求是标签必须成对出现，必须要有闭合的结束标签(个别的自闭合标签除外)，但是在这里标签的不闭合解决了一个内联元素间的间隙问题。

```html
<div class="btn-wrap">
    <button class="btn btn-reset">重置
    <button class="btn btn-commit">提交
</div>

<div class="box">
    <p>链接
    <p>链接
</div>
```

这种解决方式，我只能人为这是一种巧合，或者潜在的bug，因为隐含的一个前提是内联元素的父容器不能和内联元素是同一个类型的标记，比如实例中下面的一组标记。

```html
<p class="box">
    <p>链接
    <p>链接
</p>
```

这样就不行。这中方式，切忌，不要用，风险太高。

5. 使用浮动

不得不说，浮动，太强大了，很多问题，都可以用浮动来解决。这里的间隙问题，也可以用浮动来解决。

```html
<div class="btn-wrap">
    <button class="btn btn-reset">重置</button>
    <button class="btn btn-commit">提交</button>
</div>
```

css

```css
.btn {
    float: left;
    width: 40px;
    height: 28px;
    line-height: 28px;
    overflow: hidden;
}
```

效果

![](images/img3.png)

元素之间的间隙问题虽然解决了，但是解决就问题的同时，又带来了新的问题：浮动，按钮的父容器没有被撑开，父容器的背景色没有显示出来。如果这个时候我们还需要其他的一些效果，比如按钮居中显示等，就需要为按钮的父容器设置宽度、边距、计算按钮宽度等计算来实现，不能通过text-align:center;直接实现。所以说浮动的这种方式也不适合大规模使用。

6. 最后一种，设置font-size:0;

这里是我详细介绍的最后一种解决方案。

为内联元素的父容器设置font-size:0;同样解决问题，而且也没有带来新的问题，是一种理想的解决方案。

```htl
<div class="btn-wrap">
    <button class="btn btn-reset">重置</button>
    <button class="btn btn-commit">提交</button>
</div>
```

css样式表

```css
.btn-wrap {
    text-align: center;
    font-size: 0;
    -webkit-text-size-adjust: none;
    width: 200px;
    margin: 50px auto 5px;
    background-color: #008080;
}
.btn {
    width: 40px;
    height: 28px;
    line-height: 28px;
    overflow: hidden;
}
```

这个还是比较理想的解决方案,但是为了解决chrome的兼容性问题，需要添加一个-webkit-text-size-adjust: none;属性。

7. 其他

其他的解决方案，比如通过设置letter-spacing、word-spacing等方式，也可以解决这些问题，但是由于兼容性问题不好解决，很难做到效果的统一，所以就不再详细介绍了，但它们在某些场景下确实也是有效的解决方案。