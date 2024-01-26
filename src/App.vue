<script setup>
import {RouterView } from 'vue-router'
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';
import NavComponent from './components/NavComponent.vue'
</script>

<template>
  <HeaderComponent />
  <div class="container-fluid">
    <div class="row">
      <NavComponent/>
    <main role="main" class="col-md-9 ml-sm-auto col-lg-10 px-4">
      <RouterView />
    </main>
    
  </div>
</div>
<FooterComponent />
</template>

<style lang="scss"></style>
