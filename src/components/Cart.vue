<template>
    <div>
        <div v-if="!cart.length" class="alert alert-secondary" role="alert">
           No Product In Cart
        </div>
        <div v-if="orderPlaced" class="alert alert-success" role="alert">
            Order successfully placed!
            <button type="button" @click="() => (orderPlaced = false )" class="btn-close float-end" data-bs-dismiss="modal" aria-label="Close"></button>

        </div>
        <ul class="list-group">
            <li class="list-group-item mb-3" v-for="item in cart" :key="item.id">
                <button type="button" @click="removeItem(item.id)" class="btn-close float-end" data-bs-dismiss="modal" aria-label="Close"></button>

                <div class="d-flex mt-5 pb-5">
                    <div class="flex-shrink-0 mt-2">
                        <img :src="item.imgUrl" width="100" :alt="item.title">
                    </div>
                    <div class="flex-grow-1 ms-5 ">
                        <h5 class="mt-0">{{item.title}}</h5>
                        <button @click="reduceQty(item.id)" class="btn  btn-sm btn-secondary">-</button>
                            x {{item.qty}}
                        <button @click="addQty(item.id)" class="btn  btn-sm btn-secondary">+</button>
                    </div>
                </div>
            </li>
             <button  class="btn btn-success mt-3" v-if="cart.length" :disabled="isProcessing" @click="placeOrder">
               <span v-if="!isProcessing"> Checkout ($ {{totalPrice}})</span>
               <div v-else class="spinner-border" role="status">
                    <span class="visually-hidden">Loading...</span>
                </div>
            </button>
           
        </ul>
    </div>
</template>

<script>
import { mapActions, mapGetters } from 'vuex'; 
export default {
  data(){
    return {
        isProcessing:false,
        orderPlaced:false
    }
  },
  name: 'CartItem',
  computed:{
    ...mapGetters(['cart']),
    totalPrice(){
        return this.cart.reduce((a,b) => a+b.qty*b.price, 0);
    }
  },
  methods:{
    ...mapActions(["addQty", "reduceQty", "removeItem","emptyCart"]),
    placeOrder(){
        this.isProcessing=true;
        setTimeout(() =>{
            this.orderPlaced=true;
            this.isProcessing=false;
            this.emptyCart();
        }, 1000);
    }
  }
  
}
</script>