<script setup>
import SideBar from '@/components/SideBar.vue';
</script>

<template>
  <div class="main">
    <SideBar />
    <div>
      <h1>Adoo this is the admin</h1>
    </div>
  </div>
</template>

<style>
.main {
  display: grid;
  grid-template-columns: 1fr 4fr;
  background: var(--color-background);
  color: var(--color-text);
  min-height: 100vh;
}
</style>
