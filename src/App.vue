<template>
 <div id="root">
  <div class="todo-container">
    <div class="todo-wrap">
      <MyHeader :addTodo="addTodo" ></MyHeader>
      <MyList :todos="todos" 
	  :checkTodo="checkTodo"
	  :deleteTodo="deleteTodo"></MyList>
      <MyFooter :todos="todos" 
	  :checkAllTodo="checkAllTodo"
	  :clearAllTodo="clearAllTodo"></MyFooter>
    </div>
  </div>
</div>
</template>

<script>

import MyHeader from './components/MyHeader'
import MyList from './components/MyList'
import MyFooter from './components/MyFooter'


export default {
  name: 'App',
  components: {
    MyHeader,
    MyList,
    MyFooter
  },
  data(){
		return {
			todos:[
				{id:'001',title:'抽烟',done:true},
				{id:'002',title:'喝酒',done:false},
				{id:'003',title:'烫头',done:true}
			]
		}
	},
	methods:{
		addTodo(todoObj){
			this.todos.unshift(todoObj)
		},
		checkTodo(id){
			this.todos.forEach((todo)=>{
				if (todo.id === id) todo.done = !todo.done
			})
		},
		deleteTodo(id){
			this.todos = this.todos.filter(todo=> todo.id !== id)
		},
		// 全选或全不选
		checkAllTodo(done){
			this.todos.forEach((todo)=>{
				todo.done = done
			})
		},
		// 清除所有已完成的任务
		clearAllTodo(){
			if(confirm('确定要删除完成的任务吗')){
				this.todos = this.todos.filter(todo=>!todo.done)
			}
		}
	}
}
</script>

<style>
/*base*/
	body {
		background: #fff;
	}
	.btn {
		display: inline-block;
		padding: 4px 12px;
		margin-bottom: 0;
		font-size: 14px;
		line-height: 20px;
		text-align: center;
		vertical-align: middle;
		cursor: pointer;
		box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
		border-radius: 4px;
	}
	.btn-danger {
		color: #fff;
		background-color: #da4f49;
		border: 1px solid #bd362f;
	}
	.btn-danger:hover {
		color: #fff;
		background-color: #bd362f;
	}
	.btn:focus {
		outline: none;
	}
	.todo-container {
		width: 600px;
		margin: 0 auto;
	}
	.todo-container .todo-wrap {
		padding: 10px;
		border: 1px solid #ddd;
		border-radius: 5px;
	}

</style>
