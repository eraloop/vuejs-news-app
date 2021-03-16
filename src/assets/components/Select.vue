<template>
  <div id="app">
    <select v-model="home">
      <option v-bind:value="Homes" v-for="home in Homes" :key="home"> 
        {{home}}
      </option>
    </select>

  </div>
</template>

<script>

export default {
    props:["Homes"],
    data () {
      return {
      selected:""
    }
  }
}

</script>

<style>

</style>
