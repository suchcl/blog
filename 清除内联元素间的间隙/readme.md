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

