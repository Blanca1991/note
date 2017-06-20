#### VueX

1. 安装 
   使用npm安装 npm install vuex --save 
2. 引入 vueX
	前提是已经引入了`Vue.use(Vuex)）`；
    vueX是加载在vue的根实例上，要在app.vue中引入store  。
   
   
   		const app = new Vue({
  			el: '#app',
  			// 把 store 对象提供给 “store” 选项，这可以把 store 的实例注入所有的子组件
 			store,
 			components: { Counter },
  			template: `
    		<div class="app">
      			<counter></counter>
   	 		</div>
  			`
		})

通过在根实例中注册 store 选项，该 store 实例会注入到根组件下的所有子组件中，且子组件能通过 this.$store 访问到。



`vuex 中`

`它必须以插件的方式进行引用：
import Vuex from 'vuex';
Vue.use(Vuex); `


Mutators 事件用来驱动状态的变化 
Actions  给组件使用的函数  以此来驱动事件处理器 Mutators

应用层的状态只能通过Mutation 中的方法来修改  而派发的事件只能通过Action

从组件出发  组件调用action，在action这一层我们可以和后台数据交互，然后在action中派发Mutation。Mutation去触发状态的改变，状态的改变将触发视图的更新。

`注意事项`

数据流都是单向的
组件能够调用 action
action 用来派发 Mutation
只有 mutation 可以改变状态
store 是响应式的，无论 state 什么时候更新，组件都将同步更新




