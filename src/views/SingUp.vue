<template>
    <div>
        <h1>SingUp</h1>
        <input type="text" v-model="name" placeholder="enter your name">
        <input type="email" v-model="email" placeholder="enter your email id">
        <input type="password" v-model="password" placeholder="enter  password">
        <p></p>
        <button v-on:click="addData" type="submit">submit</button>
        <router-link class="btn" to="Login">login</router-link>

        
    </div>
</template>

<script>
import  axiOs from 'axios'
export default {

    data(){
       return{
        name:"",
        email:"",
        password:""
       }
    },
    methods: {
        async addData(){
           console.log("name ;- ",this.name,"email :- ",this.email,"password :- ",this.password);
           let result = await axiOs.post("http://localhost:3000/users",{

            name:this.name,
            email:this.email,
            password:this.password

           });
           console.log(result);
           if(result.status==201){
            alert("SingUp Done!")
            this.$router.push({name:'home'})
           }
           localStorage.setItem("user-info",JSON.stringify(result.data))
        }
    },
    mounted() {
        let user = localStorage.getItem('user-info');
        if(user){
            this.$router.push({name:'home'})
        }
        // console.log();
    },
    
}
</script>

<style scoped>
div{
    margin: 80px 10%;
    padding: 0px;
    box-sizing: border-box;
    background-color: rgba(128, 128, 128, 0.1);
    border-radius: 40px;
    height: 30rem;
    box-sizing: border-box;

}
h1{
    color: wheat;
    text-align: center;
    margin:  auto ;
    padding: 40px 0px;

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
        margin: 0% 45%;
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