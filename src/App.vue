<template>
  <div class="vue-tempalte">
    <!-- Navigation -->
    <nav class="navbar shadow bg-white rounded justify-content-between flex-nowrap flex-row fixed-top">
      <div class="container">
        <a class="navbar-brand float-left" href="#" target="_blank">
           Blockchain Dashboard
        </a>
        <ul class="nav navbar-nav flex-row float-right">
          <!--li class="nav-item">
            <router-link class="nav-link pr-3" to="/login">Sign in</router-link>
          </li-->
          <li class="nav-item" v-if="userLoggedin === false">
            <router-link class="btn btn-outline-primary" to="/">Sign up</router-link>
          </li>
          <li class="nav-item" v-if="userLoggedin === true">
            <a class="btn btn-outline-primary" href="#" v-on:click="logout">Logout</a>
          </li>
        </ul>
      </div>
    </nav>

    <!-- Main -->
    <div class="App">
      <div class="vertical-center">
        <div class="inner-block">
          <router-view />
        </div>
      </div>
    </div>
  </div>
</template>
 
 
<script>
    import axios from "axios";    
    import router from "./router";  
	
    export default {    
        name: "App",    
        data() {     
            return {     
				userLoggedin: false 				
            }    
        },    
        methods: {    
			ifUserLoggedin: function() {    
				axios.get("/api/user")    
					.then((response) => {
						let self = this; 
						self.$set(this, "userLoggedin", true);    
					})    
					.catch((errors) => {    
						console.log(errors);    
					 })    
				}, 
			logout: function (e) {
			  axios.get("/api/logout")
				.then(() => {
				  let self = this; 
				  self.$set(this, "userLoggedin", false);  
				  router.push("/")
				})
			}  
        },    
        updated() {      
            this.ifUserLoggedin();     
        }    
    }
</script>
