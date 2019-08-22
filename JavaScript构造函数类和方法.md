# JavaScript 高级

## JavaScript 面向对象

### 编程思想

- **面向过程：POP(Process-oriented programming)**
  - 面向过程就是分析出问题所需要的步骤，然后用函数把这些步骤一步一步实现，使用的时候再一个一个的一次调用就可以
  - 小项目

    **优点**：性能比面向对象高，步骤练习紧密
    **缺点**：不好维护，不易多次使用及扩展




- **面向对象：OOP (Object Oriented Programming)**

  - 面向对象就是把事物分解成一个个对象，然后由对象之间分工与合作
  - 多人合作大项目

    **优点**：易维护，可复用，可扩展，灵活性高

    **缺点**：性能没有面向过程高

### 面向对象三大特性

- **封装性**【已经把扫把功能准备好，负责开即可】
- **继承性**【继承与拖拉机，会开拖拉机就会弄这个，继承自拖拉机】
- **多态性**【可以放到一起，也可以单独拿下来，而且那个扫把坏了换哪个不影响其他的】



## 构造函数和原型

**每一个对象都有一个____proto____**

**每一个构造函数都有prototype原型对象**

### 创建函数

- 对象字面量

```js
		var obj = {
			name : '张三丰',
			age : 22
			tiaji : function () {}
		};
		console.log( obj.name );
```

- new Object()【构造函数】

```js
		var obj = new Object();
		obj.uname = '李寻欢';
		obj.age = 22;
		obj.abc = function () {}
		console.log( obj.uname );
		
		var obj1 = new Object();
		obj1.name = name;
		obj1.age = age;
```

- 自定义构造函数

```js
			function Gou (uname,age) {

			this.uname = uname;
			this.age = age;

			this.jiao = function () {
				console.log('汪汪叫');
			}

			this.tiao = function () {
				console.log('跳起来');
			}

		}

		var obj = new Gou('大黄',2);
		obj.jiao();
```

### 构造函数：constructor

**function Fn () {}**

记录是哪个构造函数创建出来的

- ____proto____和prototype都有这个属性，这个属性的作用是指回构造函数

**在JS 中，使用构造函数时要注意以下两点：**

1.构造函数用于创建某一类对象，其首字母要大写

2.构造函数要和new 一起使用才有意义

#### **new在执行时会做四件事情**

1. 在内存中创建一个新的空对象。
2. 让this指向这个新的对象。将构造函数作用域赋予新对象那；
3. 执行构造函数里面的代码，给这个新对象添加属性和方法。
4. 返回这个新对象（所以构造函数里面不需要return）。

#### 实例成员

JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的this 上添加。通过这两种方式添加的成员，就分别称为静态成员和实例成员。

- 实例成员：在构造函数内部创建的对象成员称为实例成员，只能由实例化的对象来访问

```js
	var obj = new Person('张三丰',22);	
	console.log(obj.uname);

	// console.log( Person.uname );
	Person.leibie = '人';

	console.log(Person.leibie);
	console.log(obj.leibie);
```



#### 静态成员

- 静态成员：在构造函数本上添加的成员称为静态成员，只能由构造函数本身来访问

```js
		function Person (uname, age) {
			this.uname = uname;
			this.age = age;

		this.say = function () {
			console.log(123);
		}

}
```

#### 构造函数小问题

当实例化对象的时候，属性好理解，属性名属性值，那么方法是函数，函数是复杂数据类型

那么保存的时候是保存地址，又指向函数，而每创建一个对象，都会有一个函数，每个函数都得开辟一个内

存空间，此时浪费内存了，那么如何节省内存呢，我们需要用到原型

方法放到构造函数里面，如果多次实例化，会浪费内存

```js
function Star (uname, age) {
	this.uname = uname;
	this.age = age;
	this.sing = function () {
		console.log(this.name + '在唱歌');
	}

}

var ldh = new Star('周星驰', 22);
var ldh = new Star('刘德华', 22);
```

![](F:\就业班\github\JS\assets\内存-1566175104799.jpg)

### 原型对象：prototype

**作用：是为了共享方法，从而达到节省内存**

**总结：所有的公共属性写到构造函数里面，所有的公共方法写到原型对象里面**

**疑问**：为何创建一个对象，都可以自动的跑到原型对象上找方法

因为每一个对象都有一个属性，对象原型，执行原型对象

就是一个属性，是构造函数的属性，这个属性是一个对象，我们也称呼，prototype 为原型对象。

- 每一个构造函数都有这个属性

```js
function Star (uname, age) {

​		this.uname = uname;
​		this.age = age;
​		// this.sing = function () {
​		// 	console.log(this.name + '在唱歌');
​		// }

​	}
​	Star.prototype.sing = function () {
​		console.log(this.uname + '在唱歌');
​	}

​	var zxc = new Star('周星驰', 22);
​	var ldh = new Star('刘德华', 22);
​	// console.log( Star.prototype );
​	ldh.sing();
​	zxc.sing();
```

### 对象原型：____proto____

**主要作用：指向prototype**

- 每一个实例对象都有这个属性

> ```
> 注意：____proto____是一个非标准属性，不可以拿来赋值或者设置【只读属性】
> ```

- ____proto____对象原型和原型对象prototype 是等价的
- ____proto____对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象prototype

![](F:\就业班\github\JS\assets\关系图.jpg)

	### 三者关系之间的关系

![](F:\就业班\github\JS\assets\构造函数，原型对象，对象实例关系.jpg)

- prototype：原型对象，每一个构造函数都有这个属性

- ____proto____：对象原型，每一个实例对象都有这个属性，这个属性的作用就是指向prototype

- constructor：构造函数，prototype，____proto____都有这个属性，这个属性的作用指回构造函数

## 原型链

 **作用**；提供一个成员的查找机制，或者查找规则

![](F:\就业班\github\JS\assets\原型链.jpg)



## 成员查找机制（规则）

当访问一个对象的属性（包括方法）时，首先查找这个对象自身有没有该属性。

如果没有就查找它的原型（也就是__proto__指向的prototype 原型对象）。

如果还没有就查找原型对象的原型（Object的原型对象）。

依此类推一直找到Object 为止（null）。

__proto__对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。

// console.log(Star.prototype.__proto__.__proto__);
// console.log(Object.prototype);

## 扩展内置对象

**可以通过原型对象，对原来的内置对象进行扩展自定义的方法。比如给数组增加自定义求偶数和的功能。**

```js
console.log( Array.prototype );
	// 添加求和方法
	Array.prototype.sum = function () {
		var sum = 0;
		for (var i = 0; i < this.length; i++) {
			sum += this[i];
		}
		return sum;
	}
```

# ES6中的类和对象

## 类class

- 类抽象了对象的公共部分，它泛指某一大类（class）
- 对象特指某一个，通过类实例化一个具体的对象
- 可以通过原型对象，对原来的内置对象进行扩展自定义的方法。比如给数组增加自定义求偶数和的功能。

```js
console.log( Array.prototype );
	// 添加求和方法
	Array.prototype.sum = function () {
		var sum = 0;
		for (var i = 0; i < this.length; i++) {
			sum += this[i];
		}
		return sum;
	}

	var arr = [1,2,3];
	console.log( arr.sum() );

	var newArr = [6,7,8,9];
	console.log( newArr.sum() );
```



## 创建类 class Star {};

**语法**：class 类名 {}【构造函数语法】

**注意类名首字母大写**

类要抽取公共属性方法，定义一个类

```js
class Star {
};

var ldh = new Star();
```

## 类constructor构造函数

- **注意：类里面的方法不带function，直接写既可**

- **注意：每个类里面一定有构造函数，如果没有显示定义, 类内部会自动给我们创建一个constructor() ，**

- **注意：this代表当前实力化对象，谁new就代表谁**

<u>构造函数作用：接收参数，返回实例对象，new的时候主动执行，主要放一些公共的属性</u>

**语法**：

```js
class Star {
	constructor (uname,age){
		this.uname = uname;
		this.age = age;
	}
}
```

## 类添加方法 sing(){}

- **注意：类中定义属性，调用方法都得用this**

- **注意：方法之间不能加逗号分隔，同时方法不需要添加function 关键字**

**语法**

```js
class Star {

	constructor () {}

	sing () {}

	tiao () {}

}
```

**总结：类有对象的公共属性和方法，用class创建，class里面包含constructor和方法，我们把公共属性放到constructor里面，把公共方法直接往后写既可，但是注意不要加逗号**

## 类的继承 

#### extends

语法：

```js
class Father {}

class Son extends Father{}
```

**注意：是子类继承父类**

#### super关键词

super关键字用于访问和调用对象父类上的函数。可以调用父类的构造函数，也可以调用父类的普通函数

#### 调用父类构造函数

**注意: 子类在构造函数中使用super, 必须放到this 前面(必须先调用父类的构造方法,在使用子类构造方法**

```js
class F { constructor(name, age){} }

class S extends F { constructor (name, age) { super(name,age); } }
```

#### 调用父类普通函数

**注意：如果子类也有相同的方法，优先指向子类，就近原则**

```js
class F { constructor(name, age){} say () {} }

class S extends F { constructor (name, age) { super(name,age); } say () { super.say() } }
```

#### 总结

**总结：super调用父类的属性和方法，那么查找属性和方法的原则就近原则**

类（泛指），对象（具体）

​	对象：属性和方法【对象.属性，对象.方法()】

​	类：属性和方法【new 类】

​	class 类 {

​		constructor (uname,age) {this.uname = uname; this.age = age}

​		say () {}

​		chi () {}

​	}

​	class 子类 extends 父类 {super();}

## 注意点

- **在ES6中类没有变量提升，所以必须先定义类，才能通过类实例化对象.**
- **类里面的共有属性和方法一定要加this使用.【this，对象调用属性和方法】按钮练习**
- **类里面的this指向问题.** 
- **constructor 里面的this指向实例对象, 方法里面的this 指向这个方法的调用者**

# ES5中的类和对象

## 字符串方法

> **str.trim()**
> **trim：删除字符串两侧的空白符**
>
 ## 数组方法
>
>- 迭代(遍历)方法：forEach()、map()、filter()、some()、every()；
>
>- 这些方法都是遍历数组的

## forEach( ) 方法 ==> 查询数组

**语法：**array.forEach(function(currentValue, index, arr))

currentValue：数组当前项的值
index：数组当前项的索引
arr：数组对象本身

```js
var arr = ['red','blue','yellow','orange'];

arr.forEach(function (elm,i,arrAbc) {
	console.log(elm,i,arrAbc);
});
```

## filter( ) 方法 ==> 筛选数组

**语法：**array.filter(function(currentValue, index, arr))

filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素,主要用于筛选数组

- **【直接返回一个新数组】**
- **【arr：数组对象本身回调函数里面添加return添加返回条件】**

```js
var arr = [100,66,99,123,333,33,44,66];
	var reArr = arr.filter(function (elm, a, n) {

	// console.log(elm,a, n);
	return elm % 2 == 0;

	});

	console.log(reArr);
```

## some( ) 方法 ==> 检测数组

**语法：**array.some(function(currentValue, index, arr)) ；

currentValue:数组当前项的值

some() 方法用于检测数组中的元素是否满足指定条件. 通俗点查找数组中是否有满足条件的元素

- **【注意：找到或者满足条件立刻停止】**

>- **【注意它返回值是布尔值, 如果查找到这个元素, 就返回true , 如果查找不到就返回false.】**
>
>```js
>var arr = [100,200,300,400];
>var re = arr.some(function (elm,i,arr) {
>		// console.log(elm,i,arr);
>		console.log(i);
>		return elm >= 200;
>	});
>console.log(re);
>```
>
>

## 函数的调用方式

```js
/* 1. 普通函数 */
function fn() {
	console.log('人生的巅峰');
}
 fn(); 
/* 2. 对象的方法 */
var o = {
  sayHi: function() {
  	console.log('人生的巅峰');
  }
}
o.sayHi();
/* 3. 构造函数*/
function Star() {};
new Star();
/* 4. 绑定事件函数*/
 btn.onclick = function() {};   // 点击了按钮就可以调用这个函数
/* 5. 定时器函数*/
setInterval(function() {}, 1000);  这个函数是定时器自动1秒钟调用一次
/* 6. 立即执行函数(自调用函数)*/
(function() {
	console.log('人生的巅峰');
})();
```





## 类的本质

**ES6中的class本质还是function**

ES6中的类其实就是语法糖

语法糖:语法糖就是一种**便捷写法.   简单理解**, 有两种方法可以实现同样的功能, 但是一种写法更加清晰、方便,那么这个方法就是语法糖

```js
	class Star {}
	console.log( typeof Star );
	var obj = new Star();
	console.log(obj.__proto__);
	console.log(Star.prototype);
```



## 继承

**通过构造函数+原型对象模拟实现继承，被称为组合继承。**

```
call()
调用这个函数, 并且修改函数运行时的this 指向

fun.call(thisArg, arg1, arg2, ...);call把父类的this指向子类

thisArg ：当前调用函数this 的指向对象

arg1，arg2：传递的其他参数
```

### 属性的继承 call() 构造函数

**语法Father.call( this,uname,age)**

```js
function Father (uname,age) {
			// this指向父类的实例对象
			this.uname = uname;
			this.age = age;
			// 只要把父类的this指向子类的this既可
		}
		function Son (uname, age,score) {
			// this指向子类构造函数
			// this.uname = uname;
			// this.age = age;
			// Father(uname,age);
			Father.call(this,uname,age);
			this.score = score;
		}
		Son.prototype.sing = function () {
			console.log(this.uname + '唱歌')
		}
		var obj = new Son('刘德华',22,99);
		console.log(obj.uname);
		console.log(obj.score);
		obj.sing();
```

### 方法的继承  （原型对象实现）

实现方法：**把父类的实例对象保存给子类的原型对象**

一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法。核心原理：

①将子类所共享的方法提取出来，让子类的prototype 原型对象= new 父类()  

②本质：子类原型对象等于是实例化父类，因为父类实例化之后另外开辟空间，就不会影响原来父类原型对象

③将子类的constructor 从新指向子类的构造函数	

```js
function Father () {

		}
		Father.prototype.chang = function () {
			console.log('唱歌');
		}

		function Son () {

		}
		// Son.prototype = Father.prototype;
		Son.prototype = new Father();
		var obj = new Son();
		obj.chang();

		Son.prototype.score = function () {
			console.log('考试');
		}

		// obj.score();
		// console.log(Son.prototype);
		console.log(Father.prototype);
```

**注意：一定要让Son指回构造函数**

实现继承后，让Son指回原构造函数

```js
Son.prototype = new Father();

Son.prototype.constructor = Son;
```

# 总结

- 两大编程思想：面向对象		面向过程
- 类（泛指 ）  ， 对象（具体）
- 对象：属性和方法【对象.属性  ， 对象.方法()】
- 类：属性和方法【new 类】
- class 子类 extends 父类 {super();}

- 属性放到构造函数

- 方法放到原型对象

- 原型对象：prototype，每一个构造函数都有prototype，作用：节省内存，我把方法都原型对象上

- 对象原型：____proto____，每一个实例对象都有____proto____，作用：指向原型对象

- constructor：构造函数，指回构造函数

- 原型链：实例对象==>原型对象==>原型对象，作用：查找成员规则

- ES5新增数组方法：forEach，filter，some

  



​	

