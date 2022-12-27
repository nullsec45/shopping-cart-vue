<template>
    <nav class="navbar navbar-expand-lg bg-light">
        <div class="container">
            <a class="navbar-brand" href="#">Navbar</a>
            <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavAltMarkup" aria-controls="navbarNavAltMarkup" aria-expanded="false" aria-label="Toggle navigation">
            <span class="navbar-toggler-icon"></span>
            </button>
            <div class="collapse navbar-collapse" id="navbarNavAltMarkup">
            <div class="navbar-nav ms-auto">
                <a class="nav-link active" href="#">Home</a>
                <a class="nav-link" href="#">Cart ({{totalQty}})</a>
            </div>
            </div>
        </div>
    </nav>
</template>
<script>
import { mapGetters } from 'vuex';


export default {
  name: 'HeaderItem',
  computed:{
    ...mapGetters(["cart"]),
    totalQty(){
        return this.cart.reduce((a,b) => a+b.qty,0);
    }
  }
}
</script>