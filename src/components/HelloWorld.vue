<template>
  <div class="hello">
    <table>
      <thead>
        <tr>
          <th>Id</th>
          <th>Name</th>
          <th>Address</th>
          <th>Birthday</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(item,index) in data " :key="index">
          <th>{{item.id}}</th>
          <th>{{item.name}}</th>
          <th>{{item.address}}</th>
          <th>{{item.birthday}}</th>
        </tr>
      </tbody>
    </table>
    <div>
      <div>
        <label for="">Name</label>
        <input type="text" v-model="obj.name">
      </div>
      <div>
        <label for="">Address</label>
        <input type="text" v-model="obj.address">
      </div>
      <div>
        <label for="">Birthday</label>
        <input type="text" v-model="obj.birthday">
      </div>

      <button @click="addHuman()">Add human</button>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data(){
    return{
      data:[],
      obj:{
        name:"",
        address:"",
        birthday:""
      }
    }
  },
  methods:{
    callApi(){
      axios.get("http://localhost:8080/api/v1/humans").then((response)=>{
        this.data=response.data
        console.log(response.data)
      })
    },
    addHuman(){
      axios.post("http://localhost:8080/api/v1/humans",this.obj).then((response)=>{
        console.log(response.data)
        this.callApi()
      })
    }
  },
  created(){
    this.callApi()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
