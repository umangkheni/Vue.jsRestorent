<template>
  <main>
    <TheWelcome />
  <div>
    <table border="1" >
    <tr>
      <th>ID</th>
      <th>NAME</th>
      <th>CONTACTS</th>
      <th>ADDRESS</th>
      <th>ACTIONS</th>

    </tr>
<tr v-for="item in Restaurants" :key="item.id">
      <td>{{ item.id }}</td>
      <td>{{ item.name }}</td>
      <td>{{ item.number }}</td>
      <td>{{ item.address }}</td>
      <td >
        <RouterLink  :to="'/Update/'+item.id" >Update</RouterLink> 
        <RouterLink  v-on:click="Delete(item.id)" to="/">Delete</RouterLink>
      </td>

</tr>
  </table>
  </div>
  </main>
</template>

<script >
import TheWelcome from '../components/TheWelcome.vue'
import axiOs from 'axios'


export default{

  data(){
    return{
      Restaurants:[],
      }
     },
      methods: {
        
        async Delete(id){
          let user = localStorage.getItem('user-info');
          if(user){
               let data = await axiOs.delete(`http://localhost:3000/restorunt/${id}`);
               if(data.status=200){
               this.lodData()
          }
          }else{
            alert("you ar not user login")
        }
        },
        async lodData(){
          
            let data = await axiOs.get("http://localhost:3000/restorunt");
            console.log(data);
            this.Restaurants = data.data
          
          
          
        }
      
      
     },
     mounted() {
      this.lodData()
      let user = localStorage.getItem('user-info');
      if(!user){
        
           
      }
    },
}


</script>

<style scoped>
main{
  margin: 10%;
 

}


table{
  width: 90%;
  margin: auto;
  text-align: center;
}
th{
  font-size: 125%;
  padding: 0.5%;
  color: blue;
}
td a{
  margin: 2% 5%;
}
</style>
