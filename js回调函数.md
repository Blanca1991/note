### JS回调函数

#####  一. 回调函数的作用
js代码会至上而下一条线执行下去，但是有时候我们需要等到一个操作结束之后再进行下一个操作，这时候就需要用到回调函数。

#####  二. 回调函数的解释

回调函数实际上是一种对象，他可以存储在变量中，通过参数传递给另一个函数，在函数的内部创建，从函数中反悔结果值，因为函数是内置对象，我们可以将它作为参数传递给另一个函数，到函数中执行，甚至执行后将它返回。

回调函数的英文解释为：

A callback is a function that is passed as an argument to another function and is executed after its parent function has completed.

翻译过来就是：回调函数是一个作为变量传递给另外一个函数的函数，它在主体函数执行完之后执行。

``functionA有一个参数functionB，functionB会在functionA执行完成之后被调用执行。``


#####  三. 回调函数的使用方法

	function a(callback){
		alert("函数A");
		var m=1,n=2;
	
		return callback(m,n);
	}
	
	function b(){
		alert("函数B");
		
		return m+n;
	}
	
	调用函数A
	$(function(){
	
		var result=a(b);
		alert("result:"+result);	
		
	})
	
	
在console里运行结果如下
<img src="/Users/wuxiaobo/workspace/note/image/JSdemo1.png"  width="100%" />

<img src="https://github.com/Blanca1991/note/blob/master/image/JSdemo1.png"  width="100%" />

执行顺序为：

这是parent函数a

这是回调函数B

result = 4

函数首先执行了主题函数a，之后调用了回调函数b，最后返回函数a的返回值。


如图中，b函数是a函数的一个参数，在a函数中return一个callback函数，callback函数需要使用a函数中的m、n参数。在a函数执行完毕之后，执行callback函数。b函数就是将要使用的callback函数。




 
