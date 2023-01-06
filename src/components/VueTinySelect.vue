<template>
  <div style="width: 600px">
    <div class="vue-tiny-select" @click="toggleMenu" tabindex="0" @focusout="hideMenu">
      <div class="vue-tiny-options" ref="options">
          <div v-for="(option) in options" :key="option.value">
            {{option.label}}
          </div>
      </div>
    </div>
  </div>
</template>

<script>
/* eslint-disable */

export default {
  name: "VueTinySelect.vue",
  data() {
    return {
      selected: [],
      isMenuOpen: false,
    }
  },
  props: {
    options: {
      type: Array,
      default: () => [],
      validator(val) {
        if(!Array.isArray(val)) {
          console.error('options must be an array')
          return false
        }
        let isValid = true
        val.forEach(item => {
          if(typeof item !== 'object') {
            console.error('option items must be objects')
            isValid = false
          }
          if(!item?.hasOwnProperty('label') || !item?.hasOwnProperty('value')) {
            console.error('options must have label and value property')
            isValid = false
          }
        })
        return isValid
      }
    }
  },
  methods: {
    showMenu() {
      this.$refs.options.style.display = 'block'
      this.isMenuOpen = true
    },
    hideMenu() {
      this.$refs.options.style.display = 'none'
      this.isMenuOpen = false
    },
    toggleMenu() {
      if(!this.isMenuOpen) {
        this.showMenu()
        return
      }
      this.hideMenu()
    }
  }
}
</script>
<style scoped>
.vue-tiny-select {
  position: relative;
  border: 1px solid gray;
  border-radius: .5rem;
  min-height: 60px;
  min-width: 400px;
  box-sizing: border-box;
  cursor: pointer;
}
.vue-tiny-select:focus {
  border: 1px solid #0060cc;
}
.vue-tiny-options {
  border: 1px solid gray;
  border-radius: .5rem;
  position: absolute;
  top: 100%;
  margin-top: 10px;
  min-height: 60px;
  display: none;
  width: 100%;
}
</style>