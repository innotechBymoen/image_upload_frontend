<template>
  <div>
    <!-- Ask the user for the image_id, normally this would not be what you make the user do -->
    <input type="text" placeholder="Image ID" ref="image_id_input" />
    <!-- Button for clicking -->
    <button @click="get_image">GET IMAGE</button>
    <div ref="image_container"></div>
    <p ref="message"></p>
  </div>
</template>

<script>
import axios from "axios";
export default {
  methods: {
    // Axios request
    get_image() {
      axios
        .request({
          // Standard URL and params
          url: `${process.env["VUE_APP_BASE_URL"]}/api/image`,
          params: {
            image_id: this.$refs["image_id_input"].value,
          },
          // THIS MUST BE HERE EXACTLY THE SAME
          // This lets axios know to expect a blob (one way to represent a file)
          responseType: "blob",
        })
        .then((res) => {
          // Cool built in function that allows us to take file data and create a URL for it
          // This is so we can use it for things like image src and such
          let src = URL.createObjectURL(res["data"]);

          // Insert the img tag with the src we just created above. This could also be done using Vue
          this.$refs[`image_container`].insertAdjacentHTML(
            `afterbegin`,
            `<img src="${src}">`
          );
        })
        .catch(async (err) => {
          // This function is odd. Because Axios is expecting a BLOB as a data type, we need to turn it into text to show the user the error
          // Also, notice the async on the arrow function above
          this.$refs[`message`].innerText = await err[`response`][`data`].text();
        });
    },
  },
};
</script>

<style scoped>
</style>