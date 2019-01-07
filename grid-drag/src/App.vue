<template>
  <div id="app">
   <gridDrap style="width: 300px;height: 300px">
     <gridDrapItem v-for="(item, index) in gridDrapItem" :key="index">
       <div style="box-sizing: border-box;width: 100px; height: 100px;border: 1px solid #ccc; line-height: 100px; text-align: center">{{item}}</div>
     </gridDrapItem>
   </gridDrap>
  </div>
</template>

<script>
import gridDrap from './components/grid-drap.vue';
import gridDrapItem from './components/grid-drap-item.vue';

export default {
  name: 'app',
  data(){
    return {
      gridDrapItem: [1, 2, 3, 4, 5, 6, 7, 8, 9]
    }
  },
  components: {
    gridDrap,
    gridDrapItem
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
</style>
