<template>
  <div class="offerCard" >
   
      <Offer class="tarjeta" v-for="item in $store.state.offers" :key="item.idOffer" :Offer="item"></Offer>
  </div>
</template>

<script>
import Offer from "@/components/Offer.vue";
export default {
  name: 'offerCard',
  props: {
    msg: String
  },
  data() {
     return{
      showModal: false,
    }
  },
  components: {
    Offer,
  },
  methods : {
    submit(){   
      }
    },
    showModal(){

    }
    
}
</script>
<style> 
.offerCard {
    display: flex;
    width: 100%;
    flex-wrap: wrap;
    height: 100%;
    margin-top: 50px;
    justify-content: space-evenly;
}

.tarjeta {
    width: 17%;
    height: 28%;
    background-color: white;
    border-radius: 38px;
    box-shadow: 0px 5px 10px 0px grey;
    margin-left: 5%;
    margin-right: 5%;
    margin-bottom: 5%;
}

.tarjeta img {
    width: 100%;
    height: 100px;
    border-radius: 38px 38px 0px 0px;
    object-fit: cover;
}

.infoOffer h3 {
    color: white;
    font-size: 28px;
    font-weight: 600;
    text-align: left;
    padding: 10px;
    margin-top: -45px;
    z-index: 1;
}

.infoOffer .title_offer {
    font-size: larger;
    font-weight: 600;
    text-align: center;
    width: 90%;
    margin-left: 5%;
    margin-bottom: 2%;
    margin-top: 4%;
}

.infoOffer .price {
    color: #FEA701;
    width: 90%;
    font-size: 35px;
    margin-top: 5%;
    margin-left: 5%;
    text-align: center;
    margin-bottom: 5%;
}

.redeemOffer{
  background-color: #FEA701;
  border-radius: 20px;
  color: white;
  border: 0px;
  width: 50%;
  height: 30px;
  margin-bottom: 20px;
  cursor: pointer;
}

@media only screen and (max-width: 1440px) {
  .back_difuminado {
    height: 5px;
  }
  .infoOffer h3 {
    top: 5%;
  }
}

@media only screen and (max-width: 1300px) {
  .back_difuminado {
    width: 89%;
  }

}
</style>