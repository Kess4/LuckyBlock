<template>
  <v-app-bar flat>
    <v-app-bar-title >
        <img class="logo" src="../../assets/logo.svg" width="30" height="30" />
        LuckyBlock
    </v-app-bar-title>
    <v-btn variant="outlined" color="#80C9D4" class="btn" type="submit" href="">CGU</v-btn>
  </v-app-bar>
</template>

<script setup>
  import Logo from '../../assets/logo.svg'
</script>

<style scoped>

.logo{
  margin-right: 10px;
}
.bar {
  display: contents;
}
</style>