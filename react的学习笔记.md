### React 的学习笔记

从简单的react例子开始懂得react的用法 

##### 第一个简单的例子

	<body>
		<div id="example"></div>
	</body>
	<script >
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