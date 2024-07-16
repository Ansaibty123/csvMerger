<template>
  <div class="app">
    <div class="container">
      <CsvUploader />
    </div>
  </div>
</template>

<script>
import CsvUploader from "./components/CsvUploader.vue";

export default {
  name: 'App',
  components: {
    CsvUploader,
  },
};
</script>

<style scoped>
.app {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  background-color: #f0f0f0;
}

.container {
  max-width: 600px;
  width: 100%;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
  padding: 20px;
  text-align: center;
}
</style>
