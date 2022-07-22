<template>
    <div class="todo-item" v-bind:class="{'is-complete':todo.completed}">
        <p>
        <label class="listitem">
            <input type="checkbox" v-on:change="markComplete"><i></i>
        </label>
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)" class="del">×</button></p>
    </div>
</template>

<script>
export default{
    name:"TodoItem",
    props:["todo"],
    methods:{
        markComplete(){
            this.todo.completed = !this.todo.completed;
        }
    }
}
</script>

<style scoped>
.todo-item{
    background: #fff;
    padding: 15px;
    border-bottom: 1px rgba(204, 204, 204, 0.5) solid;
}

.listitem{
    padding: 20px;
}

.listitem i{
	display: inline-block;
	width: 20px;
	height: 20px;
	border: 0.5px solid grey;
	cursor: pointer;
	border-radius: 50%;
	vertical-align: middle;
    margin-top: -3px;
    margin-left: 30px;
}

.listitem input{
	display: none;
}

.listitem input:checked+i{
	border-color: grey;
    margin-top: -11px;
}

.listitem input:checked+i::after{
	display: block;
	content: "\2714";
	text-align: center;
	border-radius: 50%;
	background: grey;
	color: #fff;
	font-size: 14px;
	padding-right: 3px;
}

.is-complete{
    text-decoration: line-through;
    color: #aaa;
    background: grey;
    opacity: 0.8;
}

.del{
    color: black;
    font-size: 150%;
    background: none;
    border: none;
    padding: 4px 40px;
    cursor: pointer;
    float: right;
}

.del:hover {
    color: #333;
}
</style>