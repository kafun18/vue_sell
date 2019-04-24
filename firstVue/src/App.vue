<template>
  <div id="app">
    <h1 v-text="title"></h1>
    <input v-model="newItem" @keyup.enter="addNew">
    <url>
      <li v-for="item in items"
        v-bind:class="{finished:item.isFinished}"
        v-on:click="toggleFinish(item)">
        {{item.label}}
      </li>
    </url>
    <p>child tells me: {{ childWords }}</p>
    <componentsA msgff='you die'
    v-on:child-tell-something="ListenToMyBoy"></componentsA>
  </div>
</template>

<script>
import Store from "./components/store.js";
import ComponentsA from './components/componentsA'
//console.log(Store);
export default {
  data: function() {
    return {
      title: "this is a tool list!",
      items: Store.fetch(),
      // [
      //   {
      //     label: "coding",
      //     isFinished: false
      //   },
      //   {
      //     label: "walking",
      //     isFinished: true
      //   }
      // ],
      liClass: "thisliclass",
      newItem: "",
      childWords: ""
    }
  },
  components: { ComponentsA },
  watch: {
    items:{
      handler:function (items){
        Store.save(items)
      },
      deep:true
    }
  },
  events: {
      'child-tell-something':function(msg){
        this.childWords = msg;
      }
  },
  methods: {
    toggleFinish: function(item) {
      // console.log(item)
      item.isFinished = !item.isFinished;
    },
    addNew: function() {
      this.items.push({
        label: this.newItem,
        isFinished: false
      });
      this.newItem = "";
      //this.title
    },
    ListenToMyBoy: function(msg){
      this.childWords = msg
    }
  } 
};
</script>

<style>
.finished {
  text-decoration: underline;
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
