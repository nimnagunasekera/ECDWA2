<template>
  <div class="main">
    <SideBar />
    <div>
      <h1>Adoo this is the admin</h1>
    </div>
  </div>
</template>

<script setup>
import SideBar from '@/components/SideBar.vue';
</script>

<style>
.main {
  display: grid;
  grid-template-columns: 1fr 4fr;
  background: var(--color-background);
  color: var(--color-text);
  min-height: 100vh;
  padding-top: 0.5rem;
  padding-bottom: 0.5rem;
}
</style>