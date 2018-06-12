<template>
  <div class="capsule login">

    <div >  <!--v-if="cartTotal > 0" -->
      <h1>Login</h1>
    
      <div class="capsule name">
       <label for="email">Email</label>
       <input id="email" type="email" v-model="stripeEmail" placeholder="name@example.com"/>
       <label for="passward">passward</label>
       <input id="passward" type="passward" v-model="passward" placeholder="passward"/>
          <nuxt-link exact to="/cart"><button>Login</button></nuxt-link>
       </div>
        <div class="capsule reg">
          <label for="registration">registration here </label>
          <nuxt-link exact to="/registration"><button>Registration</button></nuxt-link>
          </div>
       </div>
         
      <!--<div class="cartitems"v-for="item in cart"key="item">
        <div class="carttext">
          <h4>{{ item.name }}</h4>
          <p>{{ item.price | usdollar }} x {{ item.count }}</p>
          <p>Total for this item: <strong>{{ item.price * item.count }}</strong></p>
        </div>
        <img class="cartimg" :src="`/${item.img}`" :alt="`Image of ${item.name}`">
      </div>
      <div class="total">
        <h3>Total: {{ total | usdollar }}</h3>
     
        <nuxt-link exact to="/login"><button>Checkout</button></nuxt-link>
      </div>
      <app-checkout :total="total" @successSubmit="success = true"></app-checkout> -->
      
    
    

    <!--<div v-else-if="cartTotal === 0 && success === false" class="empty">
      <h1>Cart</h1>
      <h3>Your cart is empty.</h3>
      <nuxt-link exact to="/"><button>Fill er up!</button></nuxt-link>
    </div>-->

    <!--<div v-else>
      <app-success @restartCart="success = false"/>
      <h2>Success!</h2>
      <p>Your order has been processed, it will be delivered shortly.</p>
    </div>-->

  </div>
</template>

<script>
//import AppCheckout from './../components/AppCheckout.vue';
//import AppSuccess from './../components/AppSuccess.vue';

export default {
  data() {
    return {
      success: false
    };
  },
  components: {
    //AppCheckout,
    //AppSuccess
  }
   
  
};
</script>

<style scoped>
.login > div {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-content: center;
  align-items: center;
  padding: 50px;
  background: rgb(255, 255, 255);
  border-radius: 3px;
  margin-top: 10px;
  padding-bottom: 80px;
}
.name {
  border: 1px solid rgb(50, 123, 151);
  color: rgb(5, 4, 4);
  width: 500px;
  padding: 50px;
  display: flex;
  flex-direction: column;
  min-height: 10px;
  justify-content: space-between;
  text-align: center;
}
.reg {

  color: black;
  width: 500px;
  padding: 50px;
  display: flex;
  flex-direction: column;
  min-height: 10px;
  justify-content: space-between;
  text-align: center;
}


</style>
