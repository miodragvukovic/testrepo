<template>
  <main>
    <Dropdown v-bind:listData="listItems" />
    <Boxes v-bind:boxData="boxItems" />
  </main>
</template>

<script>
import Dropdown from '@/components/Dropdown.vue'
import Boxes from '@/components/Boxes.vue'

export default {
  name: 'Main',
  components: {
    Dropdown,
    Boxes
  },
  data() {
    return {
      jsonResponseData: null,
      endpoint: 'http://www.mocky.io/v2/5e8465c23000008400cf4395',
      listItems: '',
      boxItems: '',
      priceItems: ''
    }
  },
  methods: {
    getRequest() {
      this.$http.get(this.endpoint)
      .then((response) => {
        this.jsonResponseData = response.data;
        this.listItems = response.data.contract_length;
        this.boxItems = {
          data: response.data.items,
          images: response.data.assets,
          text: response.data.promo_text,
          preselectedPrice: response.data.contract_length.preselected_contract_length
        }
        this.priceItems = {
          prices: response.data.prices,
          preselectedPrice: response.data.contract_length.preselected_contract_length
        }
        // this.selectedOption = response.data.contract_length.preselected_contract_length
        console.log(this.jsonResponseData)
      }).catch(err => console.log(err));
    },
  },
  created() {
    this.getRequest()
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
