<template>
    <div>
        <form @submit="addTodo">
            <input type="text" v-model="title" name="title" placeholder="请添加待办事项...">
            <input type="submit" value="添加" class="btn">
        </form>
    </div>
</template>

<script>
// import { v4 as uuidv4 } from "uuid";
export default{
    name:"AddTodo",
    data() {
        return{
            title: ''
        }
    },
    methods:{
       addTodo(e){
        e.preventDefault();
        const newTodo = {
            title: this.title,
            completed: false
        }
        //Send up to parent
        this.$emit('add-todo', newTodo);
        this.title = '';
       } 
    }
}
</script>

<style scoped>
form{
    display: block;
    margin-top: 0em;
    background: pink;
}

input[type="text"]{
    flex: 10;
    padding: 5px;
    float: left;
    width: 50%;
    margin-left: 10%;
    margin-right: 1%;
    margin-top: 10px;
    margin-bottom: 10px;
    box-shadow: inset 0 1px 2px rgb(0 0 0 / 30%);
    display: block;
    background: white;
    border: 0;
    border-radius: 0px;
    padding: 20px;
    overflow: visible;
    font: inherit;
    box-sizing: border-box;
    transition: background .2s;
    outline: 0;
}

input[type="submit"]{
    flex: 2;
    width: 20%;
    margin-top: 10px;
    margin-bottom: 10px;
    box-shadow: 0 2px 3px rgb(0 0 0 / 40%);
    display: inline-block;
    cursor: pointer;
    background: #dc9090;
    color: #333;
    border: 0;
    border-radius: 0px;
    padding: 20px;
    font: inherit;
    box-sizing: border-box;
    transition: background .2s;
    outline: 0;
}
</style>