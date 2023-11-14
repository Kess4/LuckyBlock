<script setup>
import BlockR from '../assets/blockr.svg'
import BlockB from '../assets/blockb.svg'
import BlockG from '../assets/blockg.svg'

</script>

<template>
  <v-carousel
      :continuous="false"
      :show-arrows="false"
      hide-delimiter-background
      delimiter-icon="mdi-circle"
      height="420"
      class="car"
      color="#F9E589"
    >
    
      <v-carousel-item 
        v-for="(item, i) in items"
        :key="i"
      >
        <img :src="item.src" class="car-image" /> 
          <div class="text-h6">
              {{ item.title }} -
              {{ item.price }}
          </div>
        <!-- Ajout d'une classe .car-image pour centrer les images -->
      </v-carousel-item>
  </v-carousel>

  <div class = "infos">
    <v-banner
      lines="one"
      icon="mdi-clock-alert"
      class="my-4"
    >
      <v-banner-text>
        Date du tirage : 24/09/2029
      </v-banner-text>

    </v-banner>

    <v-banner
      lines="two"
      icon="mdi-account"
      class="my-4"
    >
      <v-banner-text>
         Nombre de participants : 50 personnes
      </v-banner-text>
    </v-banner>

  </div>

  <v-btn
      variant="flat"
      color="#5063BF"
      class="btn"
    >
      Participer
    </v-btn>
</template>

<script>
export default {
  data() {
    return {
      items: [
        { title: 'Block 1', src: BlockG, price : "0.001 ETH"},
        { title: 'Block 2', src: BlockB, price : "0.002 ETH" },
        { title: 'Block 3', src: BlockR, price : "0.005 ETH" },
      ],
    };
  },
};
</script>

<style scoped>
.car-image {
  display: flex;
  margin-left: auto;
  margin-right: auto;
  max-height: 300px; 
}
.infos{
  margin-top: 30px;

}
.btn{
  margin-top: 30px;
  margin-bottom: 35px;
  margin-right: auto;
  display: flex;
  margin-left: auto;
}

.text-h6 {
  display: flex;
  justify-content: center;
  margin-top: 30px;
}

</style>
