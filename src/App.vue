<template>
  <div id="app">
    <post-image></post-image>
    <get-images></get-images>
  </div>
</template>

<script>
import GetImages from "@/components/GetImages.vue";
import PostImage from "@/components/PostImage.vue";

export default {
  name: "App",
  components: {
    GetImages,
    PostImage,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
