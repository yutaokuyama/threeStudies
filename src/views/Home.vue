<template>
  <div class="home">
    <RotateBox msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import RotateBox from "@/components/RotateBox.vue";

export default {
  name: "Home",
  components: {
    RotateBox
  }
};
</script>
