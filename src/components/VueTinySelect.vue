<template>
  <div style="width: 400px">
    <div class="vue-tiny-select" @click="toggleMenu" tabindex="0" @focusout="hideMenu">
      <div class="vue-tiny-selected-container">
        <template v-for="item in selected">
          <div :key="item.value" class="vue-tiny-selected" :style="{backgroundColor: color}">
            <span>{{item.label}}</span>
            <span @click.stop="removeItem(item)" class="vue-tiny-close-btn">&times;</span>
          </div>
        </template>
      </div>
      <div class="vue-tiny-options" ref="options" @click.stop>
          <template v-for="(option) in options" >
            <div :style="getOptionBackgroundStyle(option)" :key="option.value" class="vue-tiny-option" @click="selectItem(option)"> {{option.label}}</div>
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
    },
    color: {
      type: String,
      default: '#0069d9'
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
    },
    removeItem(item) {
      let itemIndex = this.selected.findIndex(i => i.value === item.value)
      if(itemIndex !== -1) {
        this.selected.splice(itemIndex, 1)
      }
    },
    getOptionBackgroundStyle(item) {
      if(this.selected.findIndex(i => i.value === item.value) !== -1) {
        return {
          backgroundColor: 'rgb(243,243,243)'
        }
      }
    }
  }
}
</script>
<style lang="scss">
$select-height : 30px;
$option-height : 40px;

.vue-tiny-select {
  position: relative;
  border: 1px solid gray;
  border-radius: .5rem;
  min-height: $select-height;
  min-width: 400px;
  box-sizing: border-box;
  cursor: pointer;
}
.vue-tiny-select:focus {
  border: 2px solid #0060cc;
}
.vue-tiny-selected-container {
  display: flex;
  flex-flow: wrap;
  gap: .5rem;
  padding: .5rem;
  min-height: $select-height;
  align-items: baseline;
}
.vue-tiny-options {
  border: 1px solid gray;
  border-radius: .5rem;
  position: absolute;
  top: 100%;
  margin-top: 10px;
  display: none;
  width: 100%;
}
.vue-tiny-option {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: $option-height;
  border-bottom: 1px solid #cccccc;
}
.vue-tiny-option:hover {
  background: #f4f2f2;
}
.vue-tiny-selected {
  color: white;
  padding-left: 8px;
  border-radius: 5px;
  display: flex;
  min-height: 30px;
  align-items: center;
}
.vue-tiny-close-btn {
  border-left: 1px solid white;
  margin-left: 8px;
  width: 24px;
}
</style>