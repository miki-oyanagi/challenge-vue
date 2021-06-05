<template>
<div class="app">
  <h1>To do List✌️</h1>
  <div class="box1">
   <input type="text" name="todo" v-model="newtodo" class="input1">
   <button @click="insertTodo" class="addbutton" >追加</button>
 </div>
  <div class="box2">
    <table>
      <tr v-for="item in todolist" :key="item.id">
        <td class="">{{item.item}}</td>
        <td><input type="text" v-model="item.todo" class="input2"></td>
        <td class="update"><button @click="updateTodo(item.id,item.todo)" class="updatebutton">更新</button></td>
        <td class="delete"><button @click="deleteTodo(item.id)" class="deletebutton">削除</button></td>

      </tr>
    </table>
  </div>
</div>
</template>

<script>
import axios from "axios";
export default {
  data(){
    return{
      newtodo:"",
      todolist:[],
    };
  },
  methods:{
    async getTodo(){
      const resData =await axios.get("https://pure-lowlands-14273.herokuapp.com/api/word/");
      this.todolist = resData.data.data;
    },
    async insertTodo(){
      const sendData = {
        todo:this.newtodo,
      };
      await axios.post("https://pure-lowlands-14273.herokuapp.com/api/word/",sendData);
      await this.getTodo();
    },
    async updateTodo(id,todo){
      const sendData={
        todo:todo,
      };
      await axios.put("https://pure-lowlands-14273.herokuapp.com/api/word/" + id,sendData);
      await this.getTodo();
    },
    async deleteTodo(id){
      await axios.delete("https://pure-lowlands-14273.herokuapp.com/api/word/" + id);
    },
  },
  created(){
    this.getTodo();
  },
};
</script>


<style>
h1{
  margin-left: 10%;
}
body{
  background-color: gold
}

table{
  width: 100%;
}
.app{
  margin-top: 10%;
  margin-left: auto;
  margin-right: auto;
  background-color: white;
  width: 80%;
  height: auto;
  border-radius: 20px;
}
.box1{
  display: flex;
  height: auto;
  margin-bottom: 5%;
  width: 40%;
  margin-left: auto;
  margin-right: auto;
}
.input1{
  width: 60%;
  font-size: 20px;
}

.input2{
  width: 60%;
  font-size: 20px;
}

.box2{
  width: 40%;
  margin-left: auto;
  margin-right: auto;
}

.addbutton{
  margin-left: 25%;
  text-align: right;
  border-color:red;
  border-radius: 20%;
  background-color: white;
  color:red;
}

.updatebutton{
  border-color: hotpink;
  border-radius: 20%;
  background-color: white;
  color: hotpink;
  margin-right: 5%;
}
.deletebutton{
  border-color: blue;
  border-radius: 20%;
  background-color: white;
  color: blue;
}
@media screen and (max-width: 768px){
 
 .box1{
  width: 60%;
 }
 .box2{
  width: 60%;
}

}

</style>