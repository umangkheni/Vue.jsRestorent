<template>
    <div id="main">
        <h1>Login Page</h1>

        <input type="email" v-model="email" placeholder="enter your email id">
        <input type="password" v-model="password" placeholder="enter  password">
        <p></p>
        <button v-on:click="login" type="submit">submit</button>
        <div class="btn">
        <RouterLink to="/SingUp">SingUp</RouterLink>
        </div>


        
    </div>
</template>

<script>
import { render } from 'vue'
import axiOs from 'axios'
export default {
    name:"login",
    data(){

        return{
            email:"",
            password:""
        }
    },
    methods: {
        
       async login(){
        let result = await axiOs.get(`http://localhost:3000/users?email=${this.email}&password=${this.password} `);
            console.log(result.data);

            if(result.status==200 && result.data.length > 0){
            alert("login Done!")
            localStorage.setItem("user-info",JSON.stringify(result.data[0]))
            this.$router.push({name:'home'})
           }
           
        },
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
#main{
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
        bottom: 0%;
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
    bottom: -15px;


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
    #main{
       margin: 80px 20%; 
    }
    
}
@media only screen and (min-width: 1000px) {
    #main{
       margin: 80px 25%; 
    }
    
}
@media only screen and (min-width: 1300px) {
    #main{
       margin: 80px 30%; 
    }
    
}

</style>