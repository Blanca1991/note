### React 的学习笔记

从简单的react例子开始懂得react的用法 

##### 第一个简单的例子

	<body>
		<div id="example"></div>
	</body>
	<script >
		var WebSite = React.cretateClass({
			render:function(){
				return <a href="http://www.baidu.com">baidu</a>
			}
		});
		
		ReactDOM.render (
			<WebSite />,
			docnment.getElementById("example")
		
		)
				
	</script>
	
运行结果是
![百度 ]()
