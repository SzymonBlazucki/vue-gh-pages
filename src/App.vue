<template>
  <div id="app">
    {{ title }}<br>
    description - to be done later
    <!--<img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js + TypeScript App"/> -->
    <h2> Filtration</h2>
    <mat :initial="[1/3, 1/3, 1/3]" :matr='matrix1' />
    <h2> Fluorescence</h2>
    <mat :initial="[1/3, 1/3, 1/3]" :matr='matrix2' />
    <h2> Another type of the fluorescence</h2>
    <mat :initial="[1/3, 1/3, 1/3]" :matr='matrix3' />
    And now you can create your own operation. Just set up appropriate values in the input table and see what happens.
    <button @click='refresh = 1'>Compute</button>
   
       
    <matrixCreator /> 
    <br>
  </div>
</template>

<script lang="ts">
import { Cx } from "quantum-tensors";
import mat from './components/mat.vue';
import matrixCreator from './components/matrixCreator.vue';
//mat: () => import('../components/mat.vue')

export default({
  components: {
    mat,
    matrixCreator
  },
  data: function() {
    return {
      title: 'Project Matrix',
      matrix1: [
  ['R', 'R', Cx(1)],
  ['G', 'G', Cx(1)],
],
      matrix2: [
  ['R', 'R', Cx(1)],
  ['R', 'G', Cx(1)],
  ['R', 'B', Cx(1)]
],
       matrix3: [
  ['G', 'G', Cx(1)],
  ['G', 'B', Cx(1)],
],
      value: null,
    refresh: 0
    };
  }
   
  
})

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
