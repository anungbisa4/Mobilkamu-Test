<template>
  <div>
    <b-container>
      <b-row>
        <b-col>
          <div class="card detail">
            <b-row class="h-100">
              <b-col sm="6">
                <div class="detail-car position-relative">
                  <img class="detail-car__wrap" v-bind:src="detail.img_url" alt="">                      
                </div>
              </b-col>
              <b-col sm="6">
                <div class="h-100 p-5">
                  <h4>{{ detail.product_name }}</h4>
                  <div class="table-wrap">
                    <div class="table-colspan">
                      <h5>Spesification</h5>
                      <div class="table-detail">
                        <b-row>
                          <b-col>Brand</b-col>
                          <b-col>{{ detail.brand_name }}</b-col>                          
                        </b-row>
                      </div>
                      <div class="table-detail">
                        <b-row>
                          <b-col>Fuel</b-col>
                          <b-col>{{ detail.fuel }}</b-col>
                        </b-row>
                      </div>
                      <div class="table-price">
                        <h4>Rp. {{ detail.price }}</h4>
                      </div>
                    </div>
                  </div>
                </div>
              </b-col>
            </b-row>
          </div>
        </b-col>
      </b-row>
    </b-container>
  </div>
</template>
<script>
import axios from 'axios'
export default {
  validate ({ params }) {
    return !isNaN(+params.id)
  },
    async asyncData({ $axios, params, error }) {
    const data = await $axios.$get(`http://private-17aa77-anungbisa4.apiary-mock.com/product-detail/${+params.id}`)
    console.log(data)
    return { detail: data }
  },
};
</script>

<style>
  .detail {
    height: 550px;
  }
  .detail-car {
    height: 100%;
  }
  .detail-car__wrap {
    position: absolute;
    top: 50%;
    left: -155px;
    width: 136%;
    transform: translateY(-50%);
  }

  h5 {
    padding: 10px;
    background-color: #F5B02E;
    text-align: center;
  }

  .table-wrap {
    background-color: #F8F8F8;
  }
  .table-detail {
    padding: 10px;
    border-bottom: 1px solid #C4C4C4;
  }

  .table-price {
    padding: 10px;
    text-align: center;
    font-size: 30px;
  }
</style>
