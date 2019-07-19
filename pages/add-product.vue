<template>
        <div class="container">
            <div class="row">
                <div class="col-12">
                    <div class="card p-5">
                        <h2>Product Information</h2>
                        <form @submit.prevent="handleSubmit(product)">
                            <div class="form-group">
                                <input type="text" v-model="product.productName" id="productName" name="productName" class="form-control" :class="{ 'is-invalid': submitted && $v.product.productName.$error }" placeholder="Product Name" />
                                <div v-if="submitted && !$v.product.productName.required" class="invalid-feedback">Product Name is required</div>
                            </div>
                            <div class="form-group">
                                <input type="text" v-model="product.brandName" id="brandName" name="brandName" class="form-control" :class="{ 'is-invalid': submitted && $v.product.brandName.$error }" placeholder="Brand Name" />
                                <div v-if="submitted && !$v.product.brandName.required" class="invalid-feedback">Brand Name is required</div>
                            </div>
                            <div class="form-group">
                                <input type="text" v-model="product.fuel" id="fuel" name="fuel" class="form-control" :class="{ 'is-invalid': submitted && $v.product.fuel.$error }" placeholder="Fuel"/>
                                <div v-if="submitted && !$v.product.fuel.required" class="invalid-feedback">Fuel is required</div>
                            </div>
                            <div class="form-group">
                                <input type="number" v-model="product.price" id="price" name="price" class="form-control" :class="{ 'is-invalid': submitted && $v.product.price.$error }" placeholder="Price"/>
                                <div v-if="submitted && !$v.product.price.required" class="invalid-feedback">Price is required</div>
                            </div>
                            <div class="form-group text-center">
                                <button class="btn btn-primary rounded-full">Add Product</button>
                            </div>
                        </form>
                    </div>
                </div>
            </div>
        </div>
</template>

<script>
    import axios from 'axios';
    import Vue from 'vue'
    import { required  } from "vuelidate/lib/validators";
    import Vuelidate from 'vuelidate'
    Vue.use(Vuelidate)
    export default {
        name: "app",
        data() {
            return {
                product: {
                    productName: "",
                    brandName: "",
                    fuel: "",
                    price: "",
                },
                submitted: false
            };
        },
        validations: {
            product: {
                productName: { required },
                brandName: { required },
                fuel: { required },
                price: { required },
            }
        },
        methods: {
            handleSubmit(product) {
                this.submitted = true;
                this.$v.$touch();
                if (this.$v.$invalid) {
                    return;
                }

            axios.post('http://private-17aa77-anungbisa4.apiary-mock.com/product',{
                          "product_name": product.product_name,
                          "brand_name": product.brand_name,
                          "fuel":product.fuel,
                          "price": product.price
                          })
            .then((response) => {
              alert("success");
            })
            .catch((error) => {
              alert("Failed add product")
            })
            }
        }
    };
</script>

<style>
  h2 {
    font-size: 20px;
    font-weight: bold;
  }
  input::placeholder {
    font-size: 12px;
  }
  input {
    height: calc(2em + 0.75rem + 2px) !important;
  }
  .rounded-full {
    padding: 10px 100px;
    border-radius: 68px !important;
  }
</style>
