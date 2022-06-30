<template>
  <div class="main">
    <b-row class="row">
      <b-col md="1"></b-col>
      <b-col md="5" class="px-sm-5 p-lg-0">
        <div>
          <b-navbar variant="faded" type="light">
            <b-navbar-brand href="#" class="nav-brand">
              <img src="../assets/xing 1.png" class="d-inline-block align-top" alt="Kitten">
              <span>FastService</span>
            </b-navbar-brand>
          </b-navbar>
        </div>
        <h1 class="main-heading mt-5">Delivery cost</h1>
        <p class="main-subheading">Enter name of the city to count delivery cost</p>
        <input type="text" :class="!this.error ? 'search mt-4' : 'search-error mt-4'" placeholder="Enter name of the city" v-model="city" @keyup.enter="search">
        <button :class="!this.error ? 'search-btn' : 'error-btn'" @click="search">Enter</button>
        <p class="error mt-1" v-if="this.error">{{ this.error }}</p>
        <h4 class="table-heading my-4">Most popular cities</h4>
        <div class="table-row">
          <div class="table-col">
            <span>Nur-Sultan</span>
            <span>Zhana Turmis</span>
          </div>
          <div class="table-col">
            <span>Almaty</span>
            <span>Karaganda</span>
          </div>
          <div class="table-col">
            <span>Shymkent</span>
            <span>Kentau</span>
          </div>
          <div class="table-col">
            <span>Atyrau</span>
            <span>Aitei</span>
          </div>
          <div class="table-col">
            <span>Aktau</span>
            <span>Pavlodar</span>
          </div>
        </div>
        <footer class="desktop-footer mt-5">
          <span>All rights reserved</span>
          <br>
          <span>Fast service 2021</span>
          <div class="payment-images">
            <img src="../assets/1200px-Maestro_2016.png" alt="">
            <img src="../assets/1280px-Mastercard-logo.png" alt="">
            <img src="../assets/logo.png" alt="">
            <img src="../assets/visa-logo-icon-png_44632.png" alt="">
          </div>
        </footer>
      </b-col>
      <b-col md="6" class="deliveries" v-if="this.deliveries && !this.error">
        <b-card img-right :v-for="delivery in deliveries" class="delivery">
          <h3 :class="delivery.available ? 'delivery-header' : 'delivery-header-u'">{{ delivery.type }}</h3>
          <p v-if="!delivery.available">Not available in that city</p>
          <h4 :class="delivery.available ? 'delivery-price' : 'delivery-price-u'">{{ delivery.price }}$</h4>
        </b-card>
      </b-col>
      <b-col md="6" class="image-column" v-else>
        <img src="../assets/free-shipping 1.png" alt="" class="car-img">
        <img src="../assets/Vector 1.png" alt="" class="road-img">
        <img src="../assets/Vector 2.png" alt="" class="peshehod">
        <h4 class="img-title">Fast <br>Service</h4>
      </b-col>
    </b-row>
  </div>
</template>

<script>
export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
  data() {
    return {
      city: null,
      deliveries: null,
      error: null
    }
  },
  mounted() {

  },
  methods: {
    async search() {
      try {
        const response = await fetch(`https://qvjgl.mocklab.io/delivery/check?search=${this.city.toLowerCase()}`);
        const result = await response.json();
        this.deliveries = result;
        this.error = null;
      } catch (e){
        this.error = ("We didn't found such city. Please check spelling");
      }
    },
    wipe() {
      this.error = null;
      this.city = null;
    }
  },

}
</script>

<style scoped>

@import "../scss/style.scss";

</style>
