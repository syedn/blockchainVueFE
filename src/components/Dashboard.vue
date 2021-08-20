<template>
    <div>     
	<table>
		 <thead>
			  <tr>
			   <th>Crypto Currency</th>
			   <th>Last Trade Price  ( {{user.currency}} )</th>
			   <th>Last 24 Hour's Price  ( {{user.currency}} )</th>
			   <th>Last 24 Hour's Volume</th>
			  </tr>
		 </thead>
		 <tbody id="cryptoSection"  v-for="item in cryptoData">
			 <tr>
				<td>{{ item.cryptoCurrency }}</td>
				<td>{{ item.last_trade_price }}</td>
				<td>{{ item.price_24h }}</td>
				<td>{{ item.volume_24h }}</td>
			 </tr>
		 </tbody>  
	</table>
    </div>
	
	
</template>
<script>
    import axios from "axios";    
    import router from "../router";  
	
    export default {    
        name: "Login",    
        data() {     
            return {    
                user: { },    
                cryptoData: { }				
            }    
        },    
        methods: {    
            getUserData: function() {    
                let self = this;    
                axios.get("/api/user")    
                    .then((response) => {      
						let userInfo = response.data.user;
                        self.$set(this, "user", response.data.user);     
                    })    
                    .catch((errors) => {    
                        console.log(errors);    
                        router.push("/");    
                    });
					
            }, 
			getCryptoData: function() {
			
                let self = this    
                axios.get("/api/cryptocurrencies")    
                    .then((response) => {      
                        self.$set(this, "cryptoData", response.data.cryptoData);    
                    })    
                    .catch((errors) => {    
                        console.log(errors);   
                    })   
			} 
        },    
        mounted() {    
            this.getUserData();     
            this.getCryptoData();    //@todo: fix 
        }    
    }
</script>