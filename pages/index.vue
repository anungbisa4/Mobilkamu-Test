<template>
  <div>
    <b-container>
      <b-row>
        <b-col sm="6">
          <div class="card">
            <div class="clear-fix">
              <img class="img-icon" src="../assets/diagnostic.svg" alt="">
              <div class="content">
              <h3>Hey! Remember you have 
                  to add product in here
              </h3>
              <router-link class="link" to="/add-product">Add Product</router-link>
            </div>
            </div>
          </div>
        </b-col>
        <b-col sm="6">
          <div class="card">
            <div class="clear-fix">
              <img class="img-icon" src="../assets/garage.svg" alt="">
              <div class="content">
              <h3>You can see all product,
                  in this page
              </h3>
              <router-link class="link" to="/list-product">See All</router-link>
            </div>
            </div>
          </div>
        </b-col>
      </b-row>
      <b-row>
          <b-col sm="3" v-for="product in products">
            <div class="card">
              <div class="img">
                <img class="img-product" v-bind:src="product.img_url" alt="">
              </div>
              <div class="detail">
                <h4>{{ product.product_name }}</h4>
                <h5>Rp. {{ product.price }}</h5>
              </div>
              <router-link class="link-detail" :to="'/detail-product/' + product.id">Detail</router-link>
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
}
</script>

<style>
  .card {
    padding: 20px;
    margin-bottom: 30px;
  }
  .img{
    position: relative;
    width: 100%;
    height: 100px;
    margin-bottom: 10px;
  }
  .img-product {
    max-height: 100%;
    max-width: 100%;
    width: auto;
    height: auto;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    margin: auto;
  }
  .img-icon {
    width: 160px;
    float: left;
  }

  h3 {
    font-size: 14px;
    margin-bottom: 1.5rem;
  }
  h4 {
    font-size: 14px;
    font-weight: bold;
  }
  h5 {
    font-size: 18px;
  }

  .content {
    position: absolute;
    text-align: center;
    left: 64%;
    top: 50%;
    transform: translate(-50%,-50%);
  }

  .link {
    padding: 10px 40px;
    border-radius: 26px;
    color: #404040;
    border: 1px solid #0093DF;
    font-size: 12px;
  }

  .link:hover, .link-detail:hover {
    background-color: #0093DF;
    color: #fff;
    text-decoration: none;
    transition: 0.3s;
  }

  .link-detail {
    color: #404040;
    padding: 10px;
    text-align: center;
    width: 100%;
    border: 1px solid #0093DF;
    font-size: 12px;
  }

</style>
