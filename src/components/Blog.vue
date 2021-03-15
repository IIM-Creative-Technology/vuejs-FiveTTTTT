<template>
  <div class="blog">
    hello
    <Login />
  </div>
</template>

<script>
// import { defineComponent } from '@vue/composition-api'
import Login from "../components/Login";

export default {
  name: "Blog",
  components: {
    Login,
  },
};
</script>
