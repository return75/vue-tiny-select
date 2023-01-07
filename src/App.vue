<template>
  <div id="app">
    <vue-tiny-select :options="options"></vue-tiny-select>
  </div>
</template>

<script>
import VueTinySelect from "@/components/VueTinySelect";
export default {
  name: 'App',
  components: {
    VueTinySelect
  },
  data() {
    return {
      options: [
        {
          label: 'js',
          value: 1
        },
        {
          label: 'php',
          value: 2
        },
        {
          label: 'python',
          value: 3
        },
        {
          label: 'c++',
          value: 4
        },
        {
          label: 'ruby',
          value: 5
        },
        {
          label: 'c',
          value: 6
        },
        {
          label: 'c#',
          value: 7
        },
        {
          label: 'dart',
          value: 8
        }
      ]
    }
  }
}
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
