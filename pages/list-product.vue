<template>
  <div>
    <b-container>
      <div class="title">
        <h5>List of products</h5>
      </div>
      <b-row>
          <b-col sm="3" v-for="product in products">
            <div class="card">
              <div class="img">
                <img class="img-product" v-bind:src="product.img_url" alt="">
                <h4>{{ product.product_name }}</h4>
                <h5>Rp. {{ product.price }}</h5>
              </div>
              <router-link class="link-detail" to="/list-product">Detail</router-link>
            </div>
          </b-col>
      </b-row>
    </b-container>
  </div>
</template>

<script>
export default {
  async asyncData({ $axios }) {
    const data = await $axios.$get('http://private-17aa77-anungbisa4.apiary-mock.com/product')
    console.log(data)
    return { products: data }
  },

  methods: {

  }
}
</script>

<style>
  h5 {
    font-size: 14px;
    font-weight: bold;
  }
</style>
