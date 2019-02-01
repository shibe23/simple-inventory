<template>
  <div class="home">
    <List/>
  </div>
</template>

<script lang="ts">
import Vue from "vue";
import List from "@/components/list.vue"; // @ is an alias to /src

export default Vue.extend({
  name: "home",
  components: {
    List
  }
});
</script>
