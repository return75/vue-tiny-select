<template>
  <div style="width: 600px">
    <div class="vue-tiny-select" @click="toggleMenu" tabindex="0" @focusout="hideMenu">
      <div class="vue-tiny-selected-container">
        <template v-for="item in selected">
          <div :key="item.value" class="vue-tiny-selected">
            <span>{{item.label}}</span>
            <span></span>
          </div>
        </template>
      </div>
      <div class="vue-tiny-options" ref="options">
          <template v-for="(option) in options" >
            <div :key="option.value" class="vue-tiny-option" @click="selectItem(option)"> {{option.label}}</div>
          </template>
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
    },
    selectItem(item) {
      if(this.selected.findIndex(i => i.value === item.value) === -1) {
        this.selected.push(item)
      }
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
.vue-tiny-selected-container {
  display: flex;
  gap: .5rem;
  padding: .5rem;
  min-height: 60px;
  align-items: baseline;
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
.vue-tiny-option {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: 40px;
  border-bottom: 1px solid #cccccc;
}
.vue-tiny-option:hover {
  background: #f4f2f2;
}
.vue-tiny-selected {
  background: #0187bb;
  color: white;
  padding: 2px 6px;
  border-radius: 5px;
  display: flex;
  min-height: 30px;
  align-items: center;
}
</style>