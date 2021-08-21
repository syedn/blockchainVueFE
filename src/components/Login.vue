<template>    
	<div class="vertical-center">
    <div class="inner-block">
    <div class="vue-tempalte">
        <form v-on:submit="login">
            <h3>Sign In</h3>

            <div class="form-group">
                <label>Email address</label>
                <input type="email" class="form-control form-control-lg"  name="userEmail" />
            </div>

            <div class="form-group">
                <label>Password</label>
                <input type="password" class="form-control form-control-lg"  name="userPassword" />
            </div>
  
            <button type="submit" class="loginBtn btn btn-dark btn-lg btn-block">Sign In</button>
 
 

        </form>
    </div>
    </div>
    </div>
</template>


<script>
    import router from "../router";    
    import axios from "axios";   
	
    export default {    
        name: "Login",    
        methods: {    
            login: (e) => {    
                e.preventDefault()    
                //let userEmail = "jhondoe@gmail.com";   //@todo: change in production
                //let userPassword = "jhonPassword";   
                let userEmail = e.target.elements.userEmail.value  
                let userPassword = e.target.elements.userPassword.value   
                let login = () => {    
                    let data = {    
                        userEmail: userEmail,    
                        userPassword: userPassword    
                    }    
                    axios.post("/api/login", data)    
                        .then((response) => {    
                            router.push("/dashboard")    
                        })    
                        .catch((errors) => {    
                            console.log("Cannot log in")    
                        })    
                }    
                login()    
            }, 
            isUserLoggedin: function() {    
                axios.get("/api/user")    
                    .then((response) => {      
                        router.push("/dashboard");    
                    })    
                    .catch((errors) => {    
                        console.log(errors);    
                    })    
            }    
        },    
        mounted() {    
            this.isUserLoggedin()    
        }   
    }
</script>
