<template>
    <!--div>     
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
    </div-->
	
	 
  <div id="scene">
    <div id="left-zone">
      <ul class="list">
	   
		
        <li class="item"    v-for="cryptoItem in cryptoData">
          <input type="radio" :id="'radio_' + cryptoItem.cryptoCurrency"  name="basic_carousel" :value="cryptoItem.cryptoCurrency"/>
          <label class="" :for="'radio_' + cryptoItem.cryptoCurrency" > <i :class="'sideIcon cf cf-' + cryptoItem.icon" ></i> {{ cryptoItem.cryptoCurrency }}</label>
          
		  <div class="content content_strawberry"> <i :class="'mainIcon cf cf-' + cryptoItem.icon" ></i>
            <h1>{{ cryptoItem.cryptoCurrency }}</h1>
            <p>{{ cryptoItem.last_trade_price }} </p>
          </div>
        </li>
	  
	  
      </ul>
    </div>
    <div id="middle-border"></div>
    <div id="right-zone"></div>
  </div> 
	
	
</template>
 


<script>
    import axios from "axios";    
    import router from "../router";  
	//import '../assets/css/slider.scss';
	//import "./slider.scss";
	
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
                        self.$set(this, "user", userInfo);     
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
						let cryptoCurrencyData = response.data.cryptoData;
					
                        self.$set(this, "cryptoData", cryptoCurrencyData);    
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