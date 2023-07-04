<template>
  <div>
    <!-- Add my HTML tags for collecting the user input -->
    <input type="file" ref="upload_file" />
    <input type="text" placeholder="Description" ref="file_description" />
    <!-- Add my button for clicking -->
    <button @click="upload_image">UPLOAD</button>
    <!-- Add a simple message to show the user what happened -->
    <h3>{{ message }}</h3>
  </div>
</template>

<script>
import axios from "axios";
export default {
  // Create a variable to show the user the status of the API
  data() {
    return {
      message: "",
    };
  },
  methods: {
    upload_image() {
      // Create a new FormData to conform to the ways of file-uploading
      // In reality, this is just another key-value pair data structure
      let form = new FormData();
      // Append both the uploaded_image and description
      form.append("uploaded_image", this.$refs["upload_file"]["files"][0]);
      form.append("description", this.$refs["file_description"].value);

      // Make the axios request
      axios
        .request({
          // Standard url and method
          url: `${process.env["VUE_APP_BASE_URL"]}/api/image`,
          method: "POST",
          // THIS MUST BE HERE AND MATCH EXACTLY
          // This is what lets Flask know that you are sending a form that can contain files
          headers: {
            "Content-Type": "multipart/form-data",
          },
          // The data is simply the form we created above
          data: form,
        })
        .then((res) => {
          res;
          this.message = "Image Uploaded";
        })
        .catch((err) => {
          this.message = "Sorry, there has been an error";
          err;
        });
    },
  },
};
</script>

<style scoped>
</style>