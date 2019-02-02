<template>
  <div class="hello">
    <input type="text" maxlength="20" v-model="newItem">
    <button type="button" @click="addItem">add</button>

    <ul class="inventory">
      <li v-for="(record, index) in items" :key="index" class="inventory__list">
        <div class="inventory__list__content">
          {{ record }}
        </div>
        <div class="inventory__list__action">
          <button type="button">追加</button>
          <button type="button">削除</button>
        </div>
      </li>
    </ul>
  </div>
</template>

<script lang="ts">
import Vue from "vue";

export default Vue.extend({
  name: "List",
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
        let obj = {[`${index}`]: record }
        Object.assign(result, obj);

      })
      return result;
    }
  },
  mounted() {
    for ( let key in this.$route.query) {
      this.items.push(String(this.$route.query[key]))
    }
  }
});
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
h3 {
  margin: 40px 0 0;
}
.inventory {
  list-style-type: none;
  padding: 0;
  border: 1px solid #ddd;
  border-radius: 8px;
  max-width: 640px;
  margin: 0 auto;
  
  &__list {
    padding: 10px;
    display: flex;
    justify-content: space-between;
    &:not(:last-child){
      border-bottom : 1px dotted #ddd;
    }
    &__content {

    }
  }
}
a {
  color: #42b983;
}
</style>
