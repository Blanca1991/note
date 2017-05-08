## React 的学习笔记

从简单的react例子开始懂得react的用法 

#### 一个简单的小demo

	<!DOCTYPE html>
	<html>		
 		<head>
    		<script src="../build/react.js"></script>
    		<script src="../build/react-dom.js"></script>
    		<script src="../build/browser.min.js"></script>
  		</head>
  		
		<body>
		
			<div id="example"></div>
			
			<script type="text/babel">
			var WebSite = React.cretateClass({
				render:function(){
					return (
						<a href="http://www.baidu.com">baidu</a>
					)
				}
			});
		
			ReactDOM.render (
				<WebSite />,
				document.getElementById("example")
		
			)				
		</script>
		</body>
	</html>	
	
上面代码有两个地方需要注意。

+  `script标签的 type 属性为 text/babel`。这是因为 React 独有的 JSX 语法，跟 JavaScript 不兼容。凡是使用 JSX 的地方，都要加上 type="text/babel" 。
+ 上面代码一共用了三个库 `react.js` 、`react-dom.js` 和 `Browser.js` ，它们必须首先加载。其中，react.js 是 React 的核心库，react-dom.js 是提供与 DOM 相关的功能，Browser.js 的作用是将 JSX 语法转为 JavaScript 语法，这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。


使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo1.png"  width="100%" />


这是一个简单的例子。虽说简单，但是有两个需要注意的地方。
第一点就是声明的`WebSite`         `首字母必须大写的` 。
第二点就是在一个createClass创建的组件中`只能有一个根节点`。这个根节点可以有任意层的子节点。

错误的写法例子：
	
	var WebSite = React.cretateClass({
			render:function(){
				return (
					<h4>点击百度</4>
					<a href="http://www.baidu.com">baidu</a>
				)
			}
		}); 
		
		
如果想要实现上述两个字节点  可以在外层包裹一个父标签

正确的例子：
	
	var WebSite = React.cretateClass({
			render:function(){
				return (
					<div>
						<h4>点击百度</4>
						<a href="http://www.baidu.com">baidu</a>
					</div>
				)
			}
		}); 

其实对于`render`来说，该方法会返回一个`React组件树`，用来接受该组件树的变量名称必须首字母大写。并且该组件树`只能有一个根节点`，这也是符合实际情况的。最终这棵组件树会被`ReactDOM.render`渲染成`HTML`标签。

对于例中的<div>标签，它并不是一个真正的`DOM`节点，而是一个虚拟的DOM节点。你可以这样认为，组件树中的这些节点就是一些标记或者数据，只是React知道该如何处理这些标记或者数据。

#### JSX 语法

 `HTML`语言直接写在`JavaScript`语言之中，不加任何引号，这就是`JSX`的语法，它允许 HTML 与 JavaScript 的`混写`

	<div id="example"></div>
    <script type="text/babel">
      var names = [1, 2, 3];

      ReactDOM.render(
        <div>
        {
          names.map(function (name) {
            return <div>Hello, {name*4}!</div>
          })
        }
        </div>,
        document.getElementById('example')
      );
    </script>
    
    
 上面代码体现了 JSX 的基本语法规则：遇到`HTML`标签（以 < 开头），就用 HTML 规则解析；遇到`代码块`（以 `{` 开头），就用`JavaScript`规则解析。上面代码的运行结果如下。
 
使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo2.png"  width="50%" />

JSX 允许直接在模板插入 JavaScript 变量。如果这个变量是一个数组，则会展开这个数组的所有成员

	var arr = [
  			<h1>Hello world!</h1>,
  			<h2>React is awesome</h2>,
		];
		
	ReactDOM.render(
  		<div>{arr}</div>,
  		document.getElementById('example')
	);
 
使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo3.png"  width="50%" />


#### 组件
React 允许将代码封装成组件（component），然后像插入普通 HTML 标签一样，在网页中插入这个组件。React.createClass 方法就用于生成一个组件类

	var HelloMessage = React.createClass({
 			render: function() {
    			return <h1>Hello {this.props.name}</h1>;
  			}
		});

	ReactDOM.render(
  		<HelloMessage name="Blanca" />,
  		document.getElementById('example')
	);
	
使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo4.png"  width="50%" />

上面代码中，变量 `HelloMessage`就是一个组件类。模板插入 <HelloMessage /> 时，会自动生成 HelloMessage 的一个实例（下文的"组件"都指组件类的实例）。所有组件类都必须有自己的`render`方法，用于输出组件。

组件的用法与原生的 `HTML` 标签完全一致，可以任意加入属性，比如 <HelloMessage name="John"> ，就是 `HelloMessage` 组件加入一个 `name 属性`，值为 John。组件的属性可以在组件类的 `this.props` 对象上获取，比如 name 属性就可以通过 `this.props.name `读取。

**添加组件属性，有一个地方需要注意，就是 class 属性需要写成 className ，for 属性需要写成 htmlFor ，这是因为 class 和 for 是 JavaScript 的保留字。**



#### this.props.children

this.props 对象的属性与组件的属性一一对应，但是有一个例外，就是 this.props.children 属性。它表示组件的所有子节点  

	var NotesList = React.createClass({
        render: function() {
          return (
            <ol>
              {
                React.Children.map(this.props.children, function (child) {
                  return <li>{child}</li>;
                })
              }
            </ol>
          );
        }
      });

      ReactDOM.render(
        <NotesList>
          <span>hello</span>
          <span>world</span>
        </NotesList>,
        document.getElementById('example')
      );

上面代码的 `NoteList` 组件有两个 span 子节点，它们都可以通过 `this.props.children `读取

使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo5.png"  width="50%" />

这里需要注意， `this.props.children` 的值有三种可能：
+ 如果当前组件没有子节点，它就是 `undefined` ;
+ 如果有一个子节点，数据类型是 `object` ；
+ 如果有多个子节点，数据类型就是 `array` 。
所以，`处理 this.props.children 的时候要小心`。

React 提供一个工具方法 `React.Children` 来处理 `this.props.children` 。我们可以用 `React.Children.map` 来遍历子节点，而不用担心 this.props.children 的数据类型是 undefined 还是 object。更多的 React.Children 的方法，请参考[官方文档](https://facebook.github.io/react/docs/react-api.html)。


#### PropTypes
