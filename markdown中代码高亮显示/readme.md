
#### 怎么在markdown中添加代码作为内容中的一个区块，能使代码高亮显示并且不被解析

我主要在两个地方使用了markdown，现在说说这两个地方的实现。

第一种情况，我是在Github上使用markdown，主要是写文档，但我的一些文旦给，又大多和代码有关，就难免会粘贴一些代码到文档中，刚开始直接贴一些代中文档中，直接就被文档给解析了，我想要的效果没有出来，可是难坏了我。

后来在网上查了一些资料，终于搞明白了。

在github中的markdown文档插入代码，并使代码作为内容块高亮显示，其实很简单。在我们需要加入代码的地方连续输入模板字符串(就是键盘左上角的`,1左侧的那个不常用的键)，然后跟上要输入的代码类型，比如```html,最后在代输入结束后再连续输入3个模板字符串结束。

看下面几个例子：
```html
<div class="box">
    <div class="mod">mod</div>
    <div class="mod2">mod2</div>
    <br clear="both">
</div>
```

css代码:
```css
.box {
    width: 400px;
    margin: 0 auto;
    padding: 20px;
    background-color: #00f;
    border: 1px solid #000;
}
```
less代码:
```less
@color: #369;
@baseFontSize: 14px;
#header {
  h1 {
    font-size: @baseFontSize;
    color: @color;
    font-weight: bold;
  }
  p {
    font-size: 12px;
    a {
      text-decoration: none;
      &:hover {
        color: #333;
      }
    }
  }
}
```
js代码:
```javascript
function logTasks(env, localGulp) {
  var tree = taskTree(localGulp.tasks);
  tree.label = 'Tasks for ' + chalk.magenta(tildify(env.configPath));
  archy(tree)
    .split('\n')
    .forEach(function(v) {
      if (v.trim().length === 0) {
        return;
      }
      gutil.log(v);
    });
}
```
java代码:
```java
public class Main {
	public static void main(String[] args){
		String str = "We are happy!";
		System.out.println(spaceReplace(str));
	}

	public static String spaceReplace(String str){
		return str.replace(" ", "%20");
	}
}
```