<template>
  <section>
    <div class="container">
      <div class="flex space-between">
        <div v-for="each in boxData.data" :key="each.id" class="box">
          <div class="inner-box" v-if="each.is_featured">{{boxData.text}}</div>
          <h1>{{each.name}}</h1>
          <div class="inner-box flex">
            <figure>
              <img :src="boxData.images.tv_category">
            </figure>
            <div>
              <p v-for="promoText in each.included" :key="promoText.id">
                <span v-if="promoText.product_category == tvCategory">{{promoText.long_name}}</span>
              </p>
            </div>
          </div>
          <div class="inner-box flex">
            <figure>
              <img :src="boxData.images.net_category">
            </figure>
            <div>
            <p v-for="promoText in each.included" :key="promoText.id">
              <span v-if="promoText.product_category == netCategory">{{promoText.long_name}}</span>
            </p>
            </div>
          </div>
          <div v-if="each.promotions[0].discount_variations[0] == (preselectedData == undefined ? boxData.preselectedPrice : preselectedData)">
          <div v-html="each.promotions[0].promo_text"></div>
          <img :src="each.promotions[0].promotion_image">
          </div>
          <div>
            <p>{{each.prices.price_recurring[preselectedData || boxData.preselectedPrice]}}</p>
            <p v-if="each.prices.old_price_recurring[preselectedData || boxData.preselectedPrice] != ''">{{each.prices.old_price_recurring[preselectedData || boxData.preselectedPrice]}}</p>
            <div v-if="preselectedData == preselectedConst" v-html="each.prices.old_price_promo_text"></div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import EventBus from '@/EventBus';

export default {
  name: 'AppBody',
  props: ['boxData'],
  data() {
    return {
      netCategory: 'net',
      tvCategory: 'tv',
      preselectedData: this.boxData.preselectedPrice,
			preselectedConst: this.boxData.preselectedPrice
    }
  },
  methods: {
		onBusChange(payload) {
      this.preselectedData = payload;
    },
  },
  mounted() {
    console.log(this.preselectedData)
    EventBus.$on('selected', this.onBusChange);
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.box {
  border: 1px solid black;
  width: 100%;
  max-width: 400px;
}
.inner-box {
  border-bottom: 1px solid rgba(0,0,0,0.1);
}
figure {
  width: 80px;
}
</style>