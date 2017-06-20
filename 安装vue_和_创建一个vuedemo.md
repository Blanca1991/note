#### 参照别人贴出的vue教程，安装vue 和 创建一个vueDemo

##### 安装vue
+ 在自己的iTerm中找到创建project的文件。
+ 先用`npm -v` 查看一下版本，需要大于3.0的版本。
+ `npm install -g vue-cli` 时，会出现一直在等待npm fetchmetadata...的状态 
	
	 配置淘宝镜像：npm config set registry https://registry.npm.taobao.org
	 
+ `vue init webpack demo1`   ~~//project的文件名~~ 

	按照提示语一步一步走，如下图：
	
	<img src="https://github.com/Blanca1991/note/blob/master/image/vueSetup01.png"  width="50%" / >
	

  
+ 执行`npm install` **安依赖包**
+ 进入项目 输入` npm run dev  `   ~~//可以看到浏览器自动打开，首屏（index.html）~~ 
	下图：
	
	<img src="https://github.com/Blanca1991/note/blob/master/image/vueSetup02.png"  width="50%" / >


+ 我们的是在app上的  所以我们还要添加一个媒体查询标签    在<index.html>上
`<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no">
`    

##### 一、项目开发

1.创建首页
	在vue的src中创建views文件夹——index文件夹，存放index.vue 文件。
	
	<template>
    	<div class="titleFont">
        	vueManage
    	</div>
	</template>

	<style >
    	.titleFont{
        	font-size: 2rem;
        	color: #333;
    	}
	</style>
	
	

接着在路由中配置我们刚创建的首页，并更改一下路由的配置。
在src文件夹下的`router`文件夹中index.js文件修改路由，


	import Vue from 'vue'
	import Router from 'vue-router'
	import Hello from '@/components/Hello'
    import Index from '../views/index/index'  //**这个是我们新创建的一个index.vue文件的路由**

	Vue.use(Router)

	export default new Router({
  		routes: [
    		{
      			path: '/',
      			name: 'Index', //修改name为Index
      			component: Index  //修改component为Index
    		}
  		]
	})
	

##### 二、添加底部导航组件

底部的导航可以做成`公共组件`。在两个页面都可以引用。我们把它建在`components`文件夹下，命名为footer.vue。

文件中不需要公共的样式写在自己的vue中。

	<template >
    	<div class="footer fixed">
        	<span><router-link to='/PageOne'>pageOne</router-link></span>
        	<span><router-link  to='/'>pageTwo</router-link></span>
    	</div>
	</template>
	<style scoped>
    	.footer span{
        	display: inline-block;
        	width: 50%;
        	color:#41B883;
    	}
	</style>

	
+ 在style标签中添加`scoped`的用意是： 声明作用域，样式的效果只在本vue中起作用
+ `<router-link to='/'>`标签的作用是，实现跳转链接功能，属性to="/"既跳转到path为"/"的路径（我们在路由配置中定义的index路由）

##### 三、在首页中引入底部导航组件
在我们创建了组件之后，要使用到组件,哪个vue文件需要就在那个vue中添加。
	

	<templent>
		<div>
			<div class="titleFont">
				vueDemo
			</div>
			<footer-nav></footer-nav>
		</div>
	</templent>
	<script>
		import FooterNav from '../../components/footer.vue'   
		
		export default{
			commponents:{
				FooterNav
			}
		}
	</script>
	
+ import FooterNav from '../../components/footer.vue'    //引入组件，组件名为FooterNav 路径为 （../../components/footer.vue）
+ 局部注册  注意写在export default{}内部，compontents:{FooterNav}
+ 使用组件<footer-nav></footer-nav>,vue中，组件在js中命名必须为驼峰命名FooterNav，在使用组件的时候，使用短横线连接。

##### 四、创建PageOne的页面
###### 4.1 创建页面
pageOne.vue 是另一个模板，我们在src/views/创建一个新的文件夹pages，在pages文件下新建一个pageOne.vue

	<template >
    	<div class="pageOne tc">
        	<button>新增</button>
        	<div class="input_area">
            	<input type="text" placeholder="请输入姓名">
            	<button>确定</button>
        	</div>
        	<table>
           	 	<tr>
                	<th> 姓名 </th>
                	<th> 操作 </th>
            	</tr>
            	<tr>
                	<td> 张三 </td>
                	<td>
                    	<span>编辑</span>
                    	<span>删除</span>
                	</td>
            	</tr>
        	</table>
        	<footer-nav></footer-nav>
    	</div>
	</template>

	<script>
    	import FooterNav from '../../components/footer.vue'
    	export default{
        	components:{
            	FooterNav
        	}
    	}
	</script>

	<style scoped>
		......
	</style>

页面创建完毕，需要在路由中配置，引入，才可以通过路由／pageOne去访问。
在路由配置文router中，
	
	
	import PageOne from '../views/pages/pageOne'

	Vue.use(Router)

	export default new Router({
  		routes: [
    		{
      			path: '/',
      			name: 'Index',
      			component: Index
  			},
  			{
      			path: '/pageOne',
      			name:'pageOne',
      			component:PageOne
  			}
  		]
	})
	
	
其中 ， 在路由router中：

		import PageOneok from '../views/pages/pageOne'
		
		{
			path: '/pageOne',
      	    name: 'pageOne',
      	    component: PageOneok
			
		}
		
	
+ component: PageOneok 和 import PageOne from '../views/pages/pageOne'  是一一对应的。

+ path: '/pageOne' 和 <router-link to='/PageOne'>pageOne</router-link> 中的 to='/PageOne' 是一一对应的。

＋ name: 'pageOne' 需要定义，暂时未用到。


**在vue中，在组件中绑定v-bind:class="'isIndex':true"
绑定的方法还有**

1. ** 对象 ** 使用对象绑定时，必须加上""引号，加引号代表对应的样式，否则会将其作为对象的属性，在初始化的时候报错。
	
		v-bind:class="classObject"
		
		data:{
			classObject:{
				"class-a":true,
				"class-b":false
			}
		}




2. **数组**也可使用对象语法：

		v-bind:class="[classA, { 'classB': isB, 'classC': isC }]
		v-bind:class="[classA, { classB: isB, classC: isC }]"
		 
		 data: {  
      		classA: 'class-a',  
      		isB: true,  
      		isC: true  
    	}  
		//两个方法都可以实现
	
3. 在组件上使用v-bind:class="" ，class将被添加在根元素上面，这个元素已经存在的类不会被覆盖。
	
		<!-->子组件在父组件中：<-->
		
		<footer-nav v-bind:class="{'pageOne':isNowPage}"></footer-nav>
		
	pageOne会被渲染在子组件的div上，`pageOne的样式写在父组件中`。isNowPage的true和false来控制显示与否。
		
		
###### 4.2 编写功能
为方便我们的增删改功能，我们通过数据模拟来实现列表渲染。

###### 定义数据
在data函数下新增一个nameList数组。
	
	NameList:[{"name":"hello1"},{"name":"hello2"}] 
###### 渲染html
在html中我们开始写v-for循环语句，item 是数组元素迭代的别名。
	
	<div v-for="item in NameList"  >   
		<span>{{ item.name }}</span>
	</div>

(item, index)第二个参数可以作为当前项的索引。

	<li v-for="(item, index) in NameList">
    	{{ parentMessage }} - {{ index }} - {{ item.message }}
  	</li>

也可以用 of 替代 in 作为分隔符

	<div v-for="item of items"></div>
	
###### 添加js 


	
	
	
	
	
	
	
	





