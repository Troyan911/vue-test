
<template>
  <h1>Crypto exhchange</h1>
  <Input :changeAmount="changeAmount" :convert="convert" :favourite="favourite"/>
  <p v-if="error != ''">{{ error }}</p>
  <p v-if="result != 0" class="result-text">{{ result }}</p>

  <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
  
  <div className="selectors">
      <Selector :setCoin="setCoinFrom" :currentCoin="coinFrom"/>
      <Selector :setCoin="setCoinTo" :currentCoin="coinTo"/>
  </div>
</template>

<script>
import Input from './components/Input.vue';
import Selector from './components/Selector.vue';
import Favourite from './components/Favourite.vue';

import CryptoConvert from 'crypto-convert'

const convert = new CryptoConvert();

export default {
  components: { Input, Selector, Favourite },
  data() {
    return {
      amount: 0,
      coinFrom: '',
      coinTo: '',
      error: '',
      result: 0,
      favs: []
    }
  },
  methods: {
    favourite() {
      this.favs.push({
        from: this.coinFrom,
        to: this.coinTo
      }
      );
    },
    getFromFavs(index) {
      this.coinFrom = this.favs[index].from;
      this.coinTo = this.favs[index].to;
    },
    changeAmount(val) { this.amount = val },
    setCoinFrom(val) { this.coinFrom = val },
    setCoinTo(val) { this.coinTo = val },
    async convert() {
      if (this.amount <= 0) {
        this.error = 'Type amount greater than 0';
        return;
      }
      else if (this.coinFrom == '' || this.coinTo == '') { 
        this.error = 'Select currency';
        return;
      }
      this.error = ''

      await convert.ready();
      this.result = convert[this.coinFrom][this.coinTo](this.amount);
    }
  }
}
</script>

<style scoped>

.selectors {
  display: flex;
  justify-content:space-around;
  width: 680px;
  margin: 0 auto;
}

p {
  color: #fff;
}
</style>
