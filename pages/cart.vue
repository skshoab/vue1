<template>
  <div class="capsule cart">

    <div v-if="cartTotal > 0">
      <h1>Cart</h1>
      <div class="cartitems"v-for="item in cart"key="item">
        <div class="carttext">
          <h4>{{ item.name }}</h4>
          
          <p>{{ item.price | usdollar }} x <button  v-on:click="item.count ++"class="add" @click="addItem">+</button>{{item.count}}<button  v-on:click="item.count --" v-if="item.count > 0" class="sub" @click="subItem">-</button></p> 
       
          <p>Total for this item: <strong>{{ item.price * item.count }}</strong></p>
          
        </div>
        <img class="cartimg" :src="`/${item.img}`" :alt="`Image of ${item.name}`">
      </div>
      <div class="total">
        <h3>Total: {{ total | usdollar }}</h3>
     
        <nuxt-link exact to="/login"><button>Checkout</button></nuxt-link>
      </div>
      <app-checkout :total="total" @successSubmit="success = true"></app-checkout>
      
    </div>
    

    <div v-else-if="cartTotal === 0 && success === false" class="empty">
      <h1>Cart</h1>
      <h3>Your cart is empty.</h3>
      <nuxt-link exact to="/"><button>Fill er up!</button></nuxt-link>
    </div>

    <div v-else>
      <app-success @restartCart="success = false"/>
      <h2>Success!</h2>
      <p>Your order has been processed, it will be delivered shortly.</p>
    </div>

  </div>
</template>

<script>
//import AppCheckout from './../components/AppCheckout.vue';
import AppSuccess from './../components/AppSuccess.vue';
import AppLoader from './../components/AppLoader.vue';

export default {
  
  data() {
    return { 
      success: false
    
       
         };
  },
  components: {
    //AppCheckout,
    AppSuccess,
    AppLoader
  },
  computed: {
    cart() {
      return this.$store.state.cart;
    },
    cartTotal() {
      return this.$store.state.cartTotal;
    },
    total() {
      return Object.values(this.cart)
        .reduce((acc, el) => acc + (el.count * el.price), 0)
        .toFixed(2);
    }
  },
  filters: {
    usdollar: function(value) {
      return `$${value}`;
    }
  },
 methods: {
    addItem() {
      this.$store.commit('addItem', this.item);
    },
    subItem() {
      this.$store.commit('subItem', this.item);
    }
  }
  
};
</script>

<style scoped>
.cart > div {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  align-items: center;
  padding: 50px;
  background: white;
  border-radius: 3px;
  margin-top: 10px;
  padding-bottom: 80px;
}

.cart.empty h1,
.cart.empty h3 {
  margin-bottom: 15px;
}

.cartitems {
  padding: 30px;
  border-bottom: 1px solid #ccc;
  width: 500px;
}

.carttext {
  width: 250px;
  float: left;
  border: 1px solid rgb(140, 130, 228);
  color: rgb(5, 4, 4);
  width: 300px;
  padding: 50px;
  padding: 4px 4px !important;
  display: flex;;
  flex-direction: column;
  min-height: 10px;
  justify-content: space-between;
  text-align: left;
}

.carttext p,
.carttext h4 {
  padding: 5px;
}

.cartimg {
  width: 127px;
  border: 1px solid #ccc;
  float: right;
}

.total {
  margin: 20px 0;
}
</style>

