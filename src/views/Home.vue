<template>
  <div class="home">
    <img class="ethSVG" src="../assets/eth.svg" alt="">
    <p>View the amount of Eth in any wallet</p>
    <input type="text" v-model='walletID'>
    <button @click="getInfo()">View Eth</button><br>
    <div id="amount">{{amount}}</div>
  </div>
</template>

<script>
const web3 = new Web3(new Web3.providers.HttpProvider("https://mainnet.infura.io/v3/e8235710b20f4f039a994b4f39c0d01f"))
export default {
  name: 'Home',
  data(){
    return{
      apiUrl:'https://mainnet.infura.io/v3/e8235710b20f4f039a994b4f39c0d01f',
      walletID:'0xa485b3e631c02834A73349CFA6c5543bB0796985',
      amount:0
    }
  },
  components: {
  },
  mounted(){
   this.getInfo()
  },
  methods:{
    async getInfo(){
     let balance = await web3.eth.getBalance(this.walletID)
     this.amount =web3.utils.fromWei(balance, 'ether')+' ETH'
    }
  }
}
</script>
<style lang="scss" scoped>
.home{
  height: 500px;
  width: 100%;
  display: inline-flex;
  flex-direction: column;
  justify-content: center;
  color: white;

  .ethSVG{
    width: 200px;
    align-self: center;
  }
  button{
    width: 284px;
    padding: 3px;
    align-self: center;
  }
 input{
		display: block;
		appearance: none;
		outline: 0;
		border: 1px solid fade(white, 40%);
		background-color: fade(white, 20%);
		width: 250px;
		
		border-radius: 3px;
		padding: 10px 15px;
		margin: 0 auto 10px auto;
		display: block;
		text-align: center;
		font-size: 18px;
		
		color: rgb(0, 0, 0);
		
		transition-duration: 0.25s;
		font-weight: 300;
		
		&:hover{
			background-color: fade(white, 40%);
		}
		
		&:focus{
			background-color: white;
			width: 300px;
		}
	}
}
</style>