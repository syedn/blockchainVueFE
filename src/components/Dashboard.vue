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
	   
		
        <li class="item" v-for="cryptoItem in cryptoData">
          <input v-if="cryptoItem.icon === 'btc'"  type="radio" :id="'radio_' + cryptoItem.cryptoCurrency"  name="basic_carousel" :value="cryptoItem.cryptoCurrency"  checked="checked"/>
          <input v-if="cryptoItem.icon !== 'btc'" type="radio" :id="'radio_' + cryptoItem.cryptoCurrency"  name="basic_carousel" :value="cryptoItem.cryptoCurrency"/>
          <label class="" :for="'radio_' + cryptoItem.cryptoCurrency" > 
			<i v-if="!['efi','clout','dgld','sushi'].includes(cryptoItem.icon)" :class="'sideIcon cf cf-' + cryptoItem.icon" ></i> 
			<i v-if="['efi','clout','dgld','sushi'].includes(cryptoItem.icon)" class="sideIcon cf cf-btc" ></i> 
			
				{{ cryptoItem.cryptoCurrency }}</label>
          
		  <div class="content content_strawberry"> 
		  <i v-if="!['efi','clout','dgld','sushi'].includes(cryptoItem.icon)"  :class="'mainIcon cf cf-' + cryptoItem.icon" ></i>
		  <i v-if="['efi','clout','dgld','sushi'].includes(cryptoItem.icon)" class="mainIcon cf cf-btc" ></i> 
            <h1>{{ cryptoItem.cryptoCurrency }}</h1>
            <p>Last Traded Price {{ cryptoItem.last_trade_price }} {{user.currency}}</p>
            <p>Current Price(Last 24 Hours) {{ cryptoItem.price_24h }} {{user.currency}} </p>
            <p>Currency Volume (Last 24 Hours) {{ cryptoItem.volume_24h }} </p>
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
	
	import "@/assets/compiledcss/slider.css";
	
    export default {    
        name: "Login",    
        data() {     
            return {    
                user: { },    
                cryptoData: []			
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
					 
                        self.$set(this, "cryptoData", response.data.cryptoData);  
                    })    
                    .catch((errors) => {    
                        console.log(errors);   
                    })   
			} , 
			getCryptoDummyData: function() {
			let dummyData = [
				{   
					cryptoCurrency: 'BTC', 
					icon: 'btc', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'ETH', 
					icon: 'eth', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'XLM', 
					icon: 'xlm', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'ALGO', 
					icon: 'algo', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'EFI', 
					icon: 'efi', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'OGN', 
					icon: 'ogn', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'BTC', 
					icon: 'btc', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'CLOUT', 
					icon: 'clout', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'STX', 
					icon: 'stx', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'YFI', 
					icon: 'yfi', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'DGLD', 
					icon: 'dgld', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				},
				{   
					cryptoCurrency: 'UNI', 
					icon: 'uni', 
					price_24h:  22, //convert to local currency
					volume_24h: 21,
					last_trade_price: 45 //convert to local currency
				}
				];
                let self = this   
				self.$set(this, "cryptoData", dummyData); 
               
			} 
        },    
        mounted() {    
            this.getUserData();    
			//this.getCryptoDummyData(); //@todo: comment in production
			this.getCryptoData(); //@todo: uncomment in production    
        }
    }
</script>
