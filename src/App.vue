<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <div>
      <input type="text" v-model="inputValue" @keyup.enter="add()">
      <button @click="add()">提交</button>
    </div>
    <div>
      <ul>
        <li
          v-for="item in list"
          :class="{finshed: item.isFinshed}"
          @click="toggle(item)"
        >{{item.label}}</li>
      </ul>
    </div>
  </div>
</template>

<script>
import Store from './store.js';

export default {
  data: function() {
    return {
      title: "TodoList",
      inputValue: "",
      list: Store.fetch()
    };
  },
  watch: {
    list: {
      handler(list) {
        Store.save(list);
      },
      deep: true
    }
  },
  methods: {
    add() {
      this.list.push({label: this.inputValue, isFinshed: false});
      this.inputValue = "";
    },
    toggle(item) {
      item.isFinshed = !item.isFinshed;
    }
  }
};
</script>

<style>
.finshed {
  text-decoration: underline;
}
ul {
  width: 200px;
  margin: 20px auto;
}
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
