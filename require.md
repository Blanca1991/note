### require

require 的常用方法

1. require('http')  内置模块
2. require('./server')  "./"表示当前的路径，后面跟的是相对路径
3. require('../lib/derver) "../" 表示上一级目录，后面跟的也是相对路径

server.js
	
	var http = require('http'); 
	function start(){ 
    	server = http.createServer(function (req, res) {   
          res.writeHeader(200, {"Content-Type": "text/plain"});   
          res.end("Hello oschina\n");   
    	})   
    	server.listen(8000);   
    	console.log("httpd start @8000");   
	} 
	exports.start = start;  
	
index.js

	//路径根据自己的实际情况而定  
	var server = require("./learnNode/server"); 
	server.start(); 


##### 模块

Node 使用CommonJs模块系统。
Node 有一个简单的模块加载系统。在Node中，文件和模块一一对应。比如，在Foo.js加载同一目录中的circle.js模块。













`查看来源`

<http://www.linuxidc.com/Linux/2012-10/72627p2.ht>

<http://www.cnblogs.com/imnzq/p/6746330.html>






























