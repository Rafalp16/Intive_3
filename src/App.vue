<template>
  <div id="app">
  <div class="clearfix">
     <button class="counter_add" @click="add">Add</button>
  </div>
   <counter v-for="(counter, index) in counters" :init-value="counter.value" :init-size="counter.size" :key="counter.id" @test="remove(index)"></counter>
  </div>
</template>

<script>
import Counter from './Counter.vue'
export default {
  components: { Counter },
  name: 'app',
  data () {
    return {
      counters: [{value: 5, size: 1, id: Symbol()},{value: 95, size: 3, id: Symbol()}]
    }
  },
  methods: {
    add() {
      let value = prompt("Input starting value");
      let size = prompt("Input size");
      this.counters.push({value: value, size: size, id: Symbol()});
    },
    remove(index) {
      this.counters.splice(index, 1);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
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

.clearfix:after {
     visibility: hidden;
     display: block;
     font-size: 0;
     content: " ";
     clear: both;
     height: 0;
}
.clearfix { display: inline-block; }
* html .clearfix { height: 1%; }
.clearfix { display: block; }
</style>
