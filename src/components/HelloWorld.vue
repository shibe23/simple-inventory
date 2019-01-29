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
      if (this.newItem === '') return false;

      this.items.push(this.newItem)
      this.$router.replace({path: '/', query: this.convertArrayToObj(this.items) });
    },
    convertArrayToObj(arr: any) {
      this.newItem = "";
      let result = {}
      arr.forEach((record: any, index: number) => {
        let obj = {[`item${index}`]: record }
        Object.assign(result, obj);

      console.log(result)
      })
      return result;
    }
  },
  mounted() {
    for ( let key in this.$route.query) {
      console.log(key)
      console.log(this.$route.query[key])
      this.items.push(this.$route.query[key]) 

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
