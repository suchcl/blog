* [Vue入门](Vue入门.md)

如果有学习或接触过面相对象编程语言的同学，应该都知道类、继承、类成员等等面向对象编程一系列的术语。以前的js不具有面向对象编程，现在的js从2015年起的ES6标准，引入了class(类)的概念，同样一系列的面向对象编程的概念就都跟着过来了。

#### 类 class

class,就是一个关键词，用来创建类的。

```javascript
class className {
    ……
}
```
这样就表示一个类已经创建成功

#### 静态方法

java语言中的静态方法，就是直接在方法的前面添加一个static关键字，js中也一样。


```javascript
class Person{
	constructor(name,age,money){
		this.name = name;
		this.age = age;
		this.money = money;
		this.make = function(){
			console.log("我是" + this.name + ",今年" + this.age + "岁，1年可以挣" + this.money + "块钱。");
		}
	}
	
	/**
	 * static方法表示该方法是一个静态方法，静态方法只可以被类调用，而不能被类的实例对象调用
	 * 如果被类的实例对象调用了，则会提示该方法不存在
	 * 父类的静态方法，可以被子类继承
	 */
	static eat(){
		console.log("我没吃过早饭");
	}
}

module.exports = Person;
```

这里定义了一个class Person,在class中定义了构造方法和一个静态方法eat。

#### 静态方法的调用

静态方法，只能被被