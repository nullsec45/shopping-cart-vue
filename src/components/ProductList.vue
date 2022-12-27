<template>
 <div class="container-fluid">
    <div class="row">
        <div class="col-md-3" v-for="product in products" :key="product.id">
            <div class="card" >
                <img :src="product.imgUrl" class="card-img-top img-fluid" alt="...">
                <div class="card-body">
                    <h5 class="card-title">{{product.title}}</h5>
                    <h6 class="card-subtitle mb-2 text-muted">${{product.price}}</h6>
                    <a href="#" @click="addItemToCart(product)" class="btn btn-primary">Add to Cart</a>
                </div>
            </div>
        </div>
    </div>
 </div>
</template>
<script>
import { mapActions, mapGetters } from "vuex";

export default {
  name: 'ProductList',
  computed:{
    ...mapGetters(["products"])
  },
  methods:{
    ...mapActions((["getProducts", "addItemToCart"]))
  },
  mounted(){
    this.getProducts()
  }
}
</script>