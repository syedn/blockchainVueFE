<template>
  <div class="vue-tempalte">
    <!-- Navigation -->
    <nav class="navbar shadow bg-white rounded justify-content-between flex-nowrap flex-row fixed-top">
      <div class="container">
        <a class="navbar-brand float-left" href="#" target="_blank">
           Blockchain Dashboard
        </a>
		 
		
        <ul class="nav navbar-nav flex-row float-right" v-if="userLoggedin === false" >
          <li class="nav-item">
            <router-link class="btn btn-outline-primary" to="/">Sign up</router-link>
          </li> 
        </ul> 
		
        <ul class="nav navbar-nav flex-row float-right" v-if="userLoggedin === true" > 
		
          <li class="nav-item countryCurrency" >
				{{user.country}} ({{user.currency}})
          </li>
		  
          <li class="nav-item">
			<div class="dropdown">
			  <button class="btn btn-outline-primary">{{user.name}}</button>
			  <div class="dropdown-content">
				<a href="#">Dashboard</a>
				<a href="#">Edit Profile</a> 
				<a href="#" v-on:click="logout">Log Out</a>
			  </div>
			</div> 
          </li>
		  
        </ul> 


      </div>
    </nav>
		
	 
		

    <!-- Main -->
    <div class="App"> 
          <router-view /> 
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
				userLoggedin: false, 
				user: {}
            }    
        },    
        methods: {    
			getUserInfo: function() {    
				axios.get("/api/user")    
					.then((response) => {
					console.log("bcz I am called again")
						let self = this; 
						self.$set(this, "userLoggedin", true);    
						self.$set(this, "user", response.data.user);    
					})    
					.catch((errors) => {    
						console.log(errors);    
					 })    
				}, 
			logout: function () {
					console.log("loggedout")
			  axios.get("/api/logout")
				.then(() => { 
				  let self = this; 
				  self.$set(this, "userLoggedin", false);  
				  self.$set(this, "user", {}); 
				  router.push("/")
				})
			}  
        },    
		mounted() { this.getUserInfo();  },
        updated() {      
		//if new values are diff than the old ones 
			if(this.userLoggedin === false){
				this.getUserInfo();  
			}     
        }    
    }
</script>
