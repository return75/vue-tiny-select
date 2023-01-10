<template>
  <div id="app">
    <div style="display: flex">
      <vue-tiny-select v-model="selected" :options="options" multiple></vue-tiny-select>
      <div style="margin-left: 4rem;margin-right: 4rem; font-size: 2rem">
           <code>{{selected}}</code>
      </div>
    </div>
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
      ],
      selected: null
    }
  },
  watch: {
    selected(val) {
      console.log('val', val)
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
