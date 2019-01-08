<template>
  <div class="hello">
    <input type="text" maxlength="20" v-model="newItem">
    <button type="button" @click="addItem">add</button>

    <div v-for="(record, index) in items" :key="index">
      {{ record }}
    </div>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "HelloWorld",
  props: {
    msg: String
  },
  data(){
    return {
      newItem: '' as string,
      items: [] as string[],
    }
  },
  methods: {
    addItem() {
      this.items.push(this.newItem)
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}
</style>
