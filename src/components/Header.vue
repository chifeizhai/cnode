<template>
  <div class="header">
    <router-link
      :to="{
        name: 'root',
      }"
    >
      <img src="../assets/cnodejs_light.svg" />
    </router-link>
  </div>
</template>

<script>
export default {
  name: "Header",
};
</script>

<style scoped>
.header {
  background-color: #444444;
  height: 50px;
}
img {
  max-width: 120px;
  margin-left: 50px;
  margin-top: 10px;
}
</style>