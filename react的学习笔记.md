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
+ 上面代码一共用了三个库 react.js 、react-dom.js 和 Browser.js ，它们必须首先加载。其中，react.js 是 React 的核心库，react-dom.js 是提供与 DOM 相关的功能，Browser.js 的作用是将 JSX 语法转为 JavaScript 语法，这一步很消耗时间，实际上线的时候，应该将它放到服务器完成。


使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo1.png"  width="100%" />


这是一个简单的例子。虽说简单，但是有两个需要注意的地方。
第一点就是声明的WebSite首字母必须大写的。
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

其实对于render来说，该方法会返回一个React组件树，用来接受该组件树的变量名称必须首字母大写。并且该组件树只能有一个根节点，这也是符合实际情况的。最终这棵组件树会被ReactDOM.render渲染成HTML标签。

对于例二中的<div>标签，它并不是一个真正的DOM节点，而是一个虚拟的DOM节点。你可以这样认为，组件树中的这些节点就是一些标记或者数据，只是React知道该如何处理这些标记或者数据。

#### JSX 语法

 HTML 语言直接写在 JavaScript 语言之中，不加任何引号，这就是 JSX 的语法，它允许 HTML 与 JavaScript 的混写

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
    
    
 上面代码体现了 JSX 的基本语法规则：遇到 HTML 标签（以 < 开头），就用 HTML 规则解析；遇到代码块（以 { 开头），就用 JavaScript 规则解析。上面代码的运行结果如下。
 
使用在线编辑运行结果如图

<img src="https://github.com/Blanca1991/note/blob/master/image/demo2.png"  width="50%" />