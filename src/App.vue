<template>
  <main>
    <div class="container">
      <div class="dragNdrop-content">
        <drag-n-drop />
      </div>
    </div>
  </main>
</template>

<script setup>
import DragNDrop from './components/DragNDrop.vue';


</script>


<style scoped>
main{
    width: 100%;
  }
  .container{
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 15px;
  }
</style>
