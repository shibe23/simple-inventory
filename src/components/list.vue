<template>
  <div class="l-container">
    <div class="l-container__section h-hide-print">
      <input type="text" maxlength="20" v-model="newItem" class="input__text">
      <button type="button" @click="addItem" class="u-button_addon">追加</button>
    </div>

    <div class="l-container__section">
      <ul class="inventory">
        <li v-for="(record, index) in items" :key="index" class="inventory__list">
          <div class="inventory__list__content">
            {{ record }}
          </div>
          <div class="inventory__list__action">
            <button type="button" class="u-button h-hide-print" @click="deleteItem(index)">削除</button>
          </div>
        </li>
      </ul>
    </div>
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
      this.updateURL()
    },
    convertArrayToObj(arr: string[]) {
      this.newItem = "";
      let result = {}
      arr.forEach((record: string, index: number) => {
        let obj = {[`${index}`]: record }
        Object.assign(result, obj);

      })
      return result;
    },
    deleteItem(index: number) {
      this.items.splice(index, 1);
      this.updateURL()
    },
    updateURL() {
      this.$router.replace({path: '/', query: this.convertArrayToObj(this.items) });
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
  margin: 40px 00;
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
