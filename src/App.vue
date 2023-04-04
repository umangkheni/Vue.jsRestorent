<script >
import { RouterLink, RouterView } from 'vue-router'
import HelloWorld from './components/HelloWorld.vue'
export default{
  methods:{
    async logout(){
      localStorage.clear();
      document.getElementById('logout').style.display = 'none';
      document.getElementById('SingUp').style.display ='block' ;
      document.getElementById('login').style.display ='block' ;
      document.getElementById('add').style.display ='none' ;
    },

  },
  async mounted(){
    let user = await localStorage.getItem('user-info');
     if(user){ 
      document.getElementById('SingUp').style.display = 'none';
      document.getElementById('login').style.display = 'none';
      document.getElementById('logout').style.display  ='block';
      document.getElementById('add').style.display ='block' ;
     }
     else if(!user){
      document.getElementById('logout').style.display = 'none';
      document.getElementById('SingUp').style.display  ='block';
      document.getElementById('login').style.display ='block' ;
      document.getElementById('add').style.display ='none' ;



     }
    
},
}
</script>

<template>
  <header>
    <img alt="Vue logo" class="logo" src="@/assets/logo.svg" width="100" height="100" />

    <div class="wrapper">

      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink id="add" to="/Add">Add Restaurant</RouterLink>
        <!-- <RouterLink to="/Update">Update</RouterLink> -->
        <RouterLink id="SingUp" to="/SingUp">SingUp</RouterLink>
        <RouterLink id="login" to="/Login">Login</RouterLink>
        <RouterLink v-on:click="logout" id="logout" to="/Login">logout</RouterLink>

        


      </nav>
    </div>
  </header>
  <Router-View />
</template>

<style scoped>

header {
    display:flex;
    justify-content: space-between;
    /* position: sticky; */
  
}

.logo {
  display: block;
  margin: 1rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  display: flex;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
  font-size: 150%;
}

nav a:first-of-type {
  border: 0;
}
.wrapper{
  align-items: center;
  margin-right: 2%;

}


  header {
    display: flex;
    place-items: center;
  }

  .logo {
    margin:0.5rem;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
</style>
