
<template>
  <ul>
    <li @click="setCoin('BTC')" :className="currentCoin == 'BTC' ? 'active' : ''">BTC</li>
    <li @click="setCoin('ETH')" :className="currentCoin == 'ETH' ? 'active' : ''">ETH</li>
    <li @click="setCoin('USDT')" :className="currentCoin == 'USDT' ? 'active' : ''">USDT</li>
  </ul>
</template>

<script>
export default {
  props: {
    setCoin: {
      type: Function,
      required: true
    },
    currentCoin: {
      type: String,
      required: true
    }
  },

  // methods: {
  //   selectItem(val) { 
  //     this.setCrypto(val);
  //     this.current = val;
  //   }
  // },
  // data() { 
  //   return {
  //     current: ''
  //   }
  // }
}
</script>

<style scoped>
ul {
  list-style: none;
  width: 200px;
  padding: 0;
  border-radius: 3px;
  border: 3px solid #000;
}

ul li{
  display: block;
  background: #1a032d;
  color: #fff;
  padding: 20px 0;
}

li:hover, li.active {
  background: #620ba9;
  cursor: pointer;
}
</style>
