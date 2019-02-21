es6笔记 
#### let 和 const 

let声明的变量只在它所在的代码块有效。

		{
			let a = 1
			vat b = 2
		}
		console.log(a) // a is not defined
		console.log(b) // 2
一个{}括号就是一个let的代码块
	
		var a = [];
		for (var i = 0; i < 10; i++) {
		  a[i] = function () {
		    console.log(i);
		  };
		}
		a[6](); // 10
		
以上的代码中，变量i使用var是一个全局的变量， 所以全局只有一个变量i，，每一次的循环，变量i的值就会发生变化，console.log(i) 的这个i 就是全局变量i，a内部的所a[i]元素的值都是这个全局的i， 指向的都是同一个i，导致运行时输出的是最后一轮的i的值，也就是 10。
	
如果使用let，声明的变量仅在块级作用域内有效，最后输出的是 6。
	
		var a = [];
		for (let i = 0; i < 10; i++) {
		  a[i] = function () {
		    console.log(i);
		  };
		}
		a[6](); // 6
以上代码中，此时的变量i是用let声明的，i只在块级作用域里生效，（即，本轮的for循环中起到作用），每次的循环的i都是一个新的变量，所以最后输出的是6。**JavaScript 引擎内部会记住上一轮循环的值，初始化本轮的变量i时，就在上一轮循环的基础上进行计算。**

**另外，for循环还有一个特别之处，就是设置循环变量的那部分是一个父作用域，而循环体内部是一个单独的子作用域。**

	for (let i = 0; i < 3; i++) {
	  let i = 'abc';
	  console.log(i);
	}
	// abc
	// abc
	// abc
	
上面代码正确运行，输出了 3 次abc。这表明函数内部的变量i与循环变量i不在同一个作用域，有各自单独的作用域。

使用了let 和const 不存在变量提升的问题

**变量提升**
变量的声明会被自动移到函数或者全局代码的最顶上。移动的仅仅是声明，变量的定义赋值并不会随之提升。

是指变量可以在声明之前使用，值是undefined 

	console.log(a)  // undefined
	var a = 111  
	console.log(bar); // 报错ReferenceError
	let bar = 2; 
	
let 和const 明确了他所声明的变量 必须严格遵守 先声明后使用。
	
**暂时性死区(TDZ)**

只要块级作用域内存在let命令，它所声明的变量就“绑定”（binding）这个区域，不再受外部的影响。

	var a = 111
	if (true) {
		a = 222 // ReferenceError
		let a ;
	}
	
ES6 明确规定，如果区块中存在let和const命令，这个区块对这些命令声明的变量，从一开始就形成了封闭作用域。凡是在声明之前就使用这些变量，就会报错。

	if (true) {
	  // TDZ开始
	  tmp = 'abc'; // ReferenceError
	  console.log(tmp); // ReferenceError
	
	  let tmp; // TDZ结束
	  console.log(tmp); // undefined
	
	  tmp = 123;
	  console.log(tmp); // 123
	}

**不可重复声明**

let 不允许在相同的作用域中，重复声明同一个变量。

**块级作用域**
es6中 {{{}}}  一对花括号就是一个块级作用域
es5中只有全局作用域和函数作用域，没有块级作用域。

所以会出现以下两种情况

+ 内层变量覆盖外层变量

		var tmp = new Date();
	
		function f() {
		  console.log(tmp);
		  if (false) {
		    var tmp = 'hello world';
		  }
		}
		
		f(); // undefined
	
+ 用来计数的循环变量泄露为全局变量

		var s = 'hello';
		
		for (var i = 0; i < s.length; i++) {
		  console.log(s[i]);
		}
		
		console.log(i); // 5

es6 的块级作用域

+ 

		function f1() {
		  let n = 5;
		  if (true) {
		    let n = 10;
		  }
		  console.log(n); // 5
		}
		上面的函数有两个代码块，都声明了变量n，运行后输出 5。这表示外层代码块不受内层代码块的影响。如果两次都使用var定义变量n，最后输出的值才是 10。

+ 
	
	
		{{{{
		  {let insane = 'Hello World'}
		  console.log(insane); // 报错
		}}}};
		外层作用域无法读取内层作用域的变量

+ 
	
		{{{{
		  let insane = 'Hello World';
		  {let insane = 'Hello World'}
		}}}};
		内层作用域可以定义外层作用域的同名变量


#### const
+  const声明一个只读的常量。一旦声明，常量的值就不能改变。


		const PI = 3.1415;
		PI // 3.1415
		
		PI = 3;
		// TypeError: Assignment to constant variable.
	
+  const声明的变量不得改变值，这意味着，const一旦声明变量，就必须立即初始化，不能留到以后赋值。

		const foo;
		// SyntaxError: Missing initializer in const declaration

+ const声明的是一个对象或者数组的时候， const的变量的实质是 该对象或者数组的引用的指针。 该对象或者数组还是可以修改的。但是不能直接将新的对象或者是数组直接赋值给const 的变量，或者是 将const的变量的值修改为新的对象或者是数组的指针。

#####ES6 声明变量的六种方法
ES5 只有两种声明变量的方法：var命令和function命令。ES6 除了添加let和const命令，后面章节还会提到，另外两种声明变量的方法：import命令和class命令。所以，ES6 一共有 6 种声明变量的方法。


#### 变量的解构赋值

##### 数组的解构赋值

	es6 允许写成这样
	let [a, b, c] = [1, 2, 3];
	 
	// 按照对应位置，对变量赋值 a = 1  b=2  c =3
	
	let [foo] = [];
	let [bar, foo] = [1];
	// foo = undefined
	// 如果解构不成功，变量的值就等于undefined。
	
解构赋值 **完全解构赋值**和**非完全解构赋值**9吗 

完全解构赋值是指 = 两边的模式完全的一致 。

不完全解构赋值是指 = 左边的模式值匹配一部分等号右边的数组。
	
	let [a, [b], d] = [1, [2, 3], 4];
	a // 1
	b // 2
	d // 4
	// 解构赋值依然会成功 
	
如果等号的右边不是可以遍历的数组（或者不可遍历的结构），那就会报错
	
	let [foo] = 1;
	let [foo] = false;
	let [foo] = NaN;
	let [foo] = undefined;
	let [foo] = null;
	let [foo] = {};
	// 全部报错

解构赋值 允许指定默认值

	let [foo = true] = [];
	foo // true
	
	let [x, y = 'b'] = ['a']; // x='a', y='b'
	let [x, y = 'b'] = ['a', undefined]; // x='a', y='b'
	
**ES6 内部使用严格相等运算符（===），判断一个位置是否有值。所以，只有当一个数组成员严格等于undefined，默认值才会生效。**

	let [x = 1] = [undefined];
	x // 1
	
	let [x = 1] = [null];
	x // null

##### 对象的解构赋值
对象内部的元素 没有顺序 ，对象的解构赋值 只要等号两边的对象内有相同的属性名， 就能取到正确的值。

	let { bar, foo, zer } = { foo: "aaa", bar: "bbb" };
	foo // "aaa"
	bar // "bbb"
	zer // "undefined"

如果变量名与属性名不一致，必须写成下面这样

	let { foo: baz } = { foo: 'aaa', bar: 'bbb' };
	baz // "aaa"
	
	let obj = { first: 'hello', last: 'world' };
	let { first: f, last: l } = obj;
	f // 'hello'
	l // 'world'
	
对象的解构赋值 是下面的形式的简写

	let { foo: foo, bar: bar } = { foo: "aaa", bar: "bbb" };
	
对象的解构赋值的内部机制  是先找到同名属性，然后再赋值给对应的变量，真正被赋值的是后者 而不是前者。
	
		let { foo: baz } = { foo: "aaa", bar: "bbb" };
	baz // "aaa"
	foo // error: foo is not defined


在上述代码中，**foo是匹配模式，baz是变量**。真正被赋值的是变量baz，而不是模式foo。


对象的解构赋值也可以指定默认值，  **默认值生效的条件是，对象的属性值严格等于undefined。**

	var {x = 3} = {x: undefined};
	x // 3
	
	var {x = 3} = {x: null};
	x // null	
	
对象的嵌套赋值

	let obj = {};
	let arr = [];
	
	({ foo: obj.prop, bar: arr[0] } = { foo: 123, bar: true });
	
	foo 模式匹配 到右侧的 foo: 123 ， 将123 赋值给左侧的变量 obj.prop ， obj.prop = 123 ，所得obj = {prop: 123} 。 arr 同理的到 arr=[true]。
	
**如果解构失败，变量的值等于undefined。**

将一个已经声明的变量用于解构赋值，必须要特别的小心。

下面代码会报错
	
	let x
	{x} = {x: 1}

因为js引擎会将{x}视作是一个代码块，从而发生语法错误。 只有不将{}写在首行，避免js将其解释为代码块，才能解决这个问题。

	let x
	({x} = {x: 1})

将整个解构赋值语句，放在一个圆括号里面，就可以正确执行

在js中数组也是对象，数组也阔以和对象解构

	let arr = [0,1,2]
	let {0: a, [arr.lenght-1]: b} = arr
	a = 0  b = 2
	
	在此代码中 arr[0] = 0    arr[arr.lenght - 1] = 2

##### 字符串的解构赋值 

字符串在解构赋值的时候  首先会被转换成一个数组 

	const [a, b, c, d, e] = 'hello';
	a b c d e 分别是 hello
	
	let {length : len} = 'hello';  length 是hello的长度  len = 5
	
##### 函数参数的解构赋值

函数的参数的解构赋值是 对函数的入参的参数 解构
	
	function add([x, y]){
	  return x + y;
	}
	
	add([1, 2]); // 3

	函数add的参数表面上是一个数组，但在传入参数的那一刻，数组参数就被解构成变量x和y。
	
	
#####  解构赋值的用途

+ 交换变量 
	
	let x = 1;
	let y = 2;
	
	[x, y] = [y, x];   x：2  y：1
	
+  从函数返回多个值 

	// 返回一个数组

	function example() {
	  return [1, 2, 3];
	}
	let [a, b, c] = example();
	
	// 返回一个对象
	
	function example() {
	  return {
	    foo: 1,
	    bar: 2
	  };
	}
	let { foo, bar } = example();


+ 函数参数的定义

	方便将一组参数和变量一一对应
		
	// 参数是一组有次序的值
	function f([x, y, z]) { ... }
	f([1, 2, 3]);
	
	// 参数是一组无次序的值
	function f({x, y, z}) { ... }
	f({z: 3, y: 2, x: 1});

+  提取json数据

	let jsonData = {
	  id: 42,
	  status: "OK",
	  data: [867, 5309]
	};
	
	let { id, status, data: number } = jsonData;
	
	console.log(id, status, number);
	// 42, "OK", [867, 5309]
	
+  遍历 Map 结构

	/////


#### 字符串的扩展

1.  字符的 Unicode 表示法 （es6中将码点放在大括号里 正确解读到字符串）
	 
	 "𠮷" 的表示法  "\uD842\uDFB7"  ->  "\u{20BB7}"
	 "ABC" 的表示法 "\u{41}\u{42}\u{43}"
	 
 	 let hello = 123;   hell\u{6F} // 123
 	 
 	 '\u{1F680}' === '\uD83D\uDE80'  // true
 	 
 	 
 	 JavaScript 共有 6 种方法可以表示一个字符
 	 '\z' === 'z'  // true
	 '\172' === 'z' // true
	 '\x7A' === 'z' // true
	 '\u007A' === 'z' // true
	 '\u{7A}' === 'z' // true
	 
2. codePointAt()

		var s = "𠮷";
		s.codePointAt(0) // 134071
	
	**codePointAt() 获取的码点是十进制值**  可以使用toString(16) 转换为16进制值
	s.codePointAt(0).toString(16) // "20bb7" 
	

使用codePointAt() 的时候， 如果  s = '𠮷a'。 '𠮷'是需要4个字节储存。（JavaScript 内部，字符以 UTF-16 的格式储存，每个字符固定为2个字节，对于那些需要4个字节储存的字符（Unicode 码点大于0xFFFF的字符），JavaScript 会认为它们是两个字符。）。
	
		let s = '𠮷a';
		for (let ch of s) {
		  console.log(ch.codePointAt(0).toString(16));
		}
		// 20bb7
		// 61
		
codePointAt方法是测试一个字符由两个字节还是由四个字节组成的最简单方法

	function is32Bit(c) {
     return c.codePointAt(0) > 0xFFFF;
   }

	is32Bit("𠮷") // true
	is32Bit("a") // false
	
**fromCodePoint方法定义在String对象上，而codePointAt方法定义在字符串的实例对象上。**

3. 
	
	















Symbol


js的六大数据类型 null string number object undefined Boolean es6新增的 Symbol 这个新的数据类型。

Symbol的值通过 Symbol函数生成一个唯一的变量。

	let a = Symbol('apple') // typeof s -> Symbol
	apple 是对a变量的描述。 a.toString()  -> Symbol('apple')
	let b = Symbol('apple') // a === b -> false 
	每一个Symbol定义的变量都是唯一的， Symbol值可以显式转为字符串, Symbol 值也可以转为布尔值，但是不能转为数值。 
	
	let a = Symbol('apple')
	a = 'big apple'
	
	console.log(' eat' + a) 报错 做字符运算时 不能直接相加 转化为string后再做字符串相加
	
如果Symbol值作为对象的属性 
	
	创建方法为
	let mySymbol = Symbol('firstSymbol')
	let myObject = {}
	
	myObject[mySymbol] = 'Hello!'; // 第一种方法
	
	myObject = {
	  [mySymbol]: 'Hello!'
	}; // 第二种方法
	
	Object.defineProperty(myObject, mySymbol, { value: 'Hello!' }); // 第三种方法
	
	myObject[mySymbol] = 'hello'  创建不能使用.运算符创建，因为.运算符后跟的是string， 而不是一个 Symbol 值。 

	let s = Symbol();

	let obj = {
	  [s]: function (arg) { ... }
	};
	采用增强的对象写法会更简洁
	let obj = {
	  [s](arg) { ... }
	};
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	