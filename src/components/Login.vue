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

            <button type="submit" class="btn btn-dark btn-lg btn-block">Sign In</button>

            <p class="forgot-password text-right mt-2 mb-4">
                <a href="#">Forgot password ?</a>
            </p>

            <div class="social-icons">
                <ul>
                    <li><a href="#"><i class="fa fa-google"></i></a></li>
                    <li><a href="#"><i class="fa fa-facebook"></i></a></li>
                    <li><a href="#"><i class="fa fa-twitter"></i></a></li>
                </ul>
            </div>

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
                let userEmail = "jhondoe@gmail.com";   //@todo: change in production
                let userPassword = "jhonPassword";   
                //let userEmail = e.target.elements.userEmail.value  
                //let userPassword = e.target.elements.userPassword.value   
                let login = () => {    
                    let data = {    
                        userEmail: userEmail,    
                        userPassword: userPassword    
                    }    
                    axios.post("/api/login", data)    
                        .then((response) => {    
                            console.log("Logged in");  
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
