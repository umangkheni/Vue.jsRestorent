<template>
    <div main>
      <h1>Update Restaurant</h1>

      


        <form action="Update">
            <input v-model="name" type="text" placeholder="Enter Restaurants Name">
            <input v-model="number" type="text" placeholder="Enter Restaurants number">
            <input v-model="address" type="text" placeholder="Enter Restaurants Address">
            

       <button type="button" v-on:click="Update" class="Update">Update Restaurant</button>
        </form>


        
    </div>
</template>


<script>
import axiOs from 'axios'
export default {
    data(){
       return{
         
        name:'',
        number:'',
        address:''
        
       }
    },
    methods:{
        async Update(){
            let user = localStorage.getItem('user-info');
          if(user){
        let id  = this.$route.params.id;
        let newData = await axiOs.put(`http://localhost:3000/restorunt/${id}` , {
            name:this.name,
            number:this.number,
            address:this.address
        });
        console.log(newData);
        this.$router.push({name:'home'});
        }else{
            alert("you ar not user login")
          }
    }
    

    },
    async mounted() {
        let id  = this.$route.params.id;
        let data = await axiOs.get(`http://localhost:3000/restorunt/${id}`);
        let Result = data.data;
        this.oldData = data.data;
        this.name = Result.name;
        this.number = Result.number;
        this.address = Result.address;

    },
    // methods:{
    //     async Update(){
    //     let newData = await axiOs.put(`http://localhost:3000/restorunt/${id}`,{

    //         name:this.name,
    //         number:this.number,
    //         address:this.address
    //     });
    //     console.log(newData);
    //     this.$router.push({name:'home'})
    //     }

    // }
    
}
</script>

<style scoped>

h1{
    text-align: center;
    font-size: 3rem;
    padding-top: 20px;
}

div{
    margin: 20px 10%;
    padding: 0px;
    box-sizing: border-box;
    background-color: rgba(128, 128, 128, 0.1);
    border-radius: 40px;
    height: 28rem;
    box-sizing: border-box;

}
input{
    display: block;
    width: 60%;
    margin-left: auto;
    margin-right: auto;
    margin-top: 20px !important;
    height: 40px;
    border: 2px solid grey;
    padding-left: 20px;
    font-size: 110%;
    border-radius: 10px;


}
.btn{
        margin: 0% 20%;
        bottom: -5%;
}
button{
    display: block;
    width: 60%;
    margin-left: auto;
    margin-right: auto;
    margin-top: 30px !important;
    height: 40px;
    margin-bottom: 40px;
    font-size: 110%;
    border-radius: 20px;
    bottom: -40px;


}
button:hover{
    background-color: blueviolet;
    border: 3px solid blue;
        font-size: 130%;
        font-weight: 650;
        color: aliceblue;
        box-shadow: 0px 0px 20px 3px blueviolet;


}
@media only screen and (min-width: 800px) {
    div{
       margin: 80px 20%; 
    }
    
}
@media only screen and (min-width: 1000px) {
    div{
       margin: 80px 25%; 
    }
    
}
@media only screen and (min-width: 1300px) {
    div{
       margin: 80px 30%; 
    }
    
}
</style>