<template>
  <div style="width: 400px">
    <div class="vue-tiny-select" @click="toggleMenu" tabindex="0" @focusout="hideMenu">
      <div class="vue-tiny-selected-container">
        <template v-if="multiple">
          <template v-for="item in selected">
            <div :key="item.value" class="vue-tiny-selected" :style="{backgroundColor: color}">
              <span>{{item.label}}</span>
              <span @click.stop="removeItem(item)" class="vue-tiny-close-btn">&times;</span>
            </div>
          </template>
        </template>
        <template v-else>
          <div class="vue-tiny-single-selected">{{firstArrayIndex}}</div>
        </template>
      </div>
      <div class="caret-and-clear-btn">
        <div class="caret-down" :style="{transform: isMenuOpen ? 'rotateZ(180deg)': ''}"></div>
        <div v-if="selected.length" class="vue-tiny-clear-btn" @click="clearSelected">
          &times;
        </div>
      </div>
      <div class="vue-tiny-options" ref="options" @click.stop>
          <template v-for="(option) in options" >
            <div :style="getOptionBackgroundStyle(option)" :key="option.value" class="vue-tiny-option" @click="toggleSelect(option)"> {{option.label}}</div>
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
    multiple: {
      type: Boolean,
      default: false
    },
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
  computed: {
    firstArrayIndex() {
      return this.selected.at(0)?.label
    }
  },
  methods: {
    updateModel(model) {
      this.$emit('input', model)
    },
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
    toggleSelect(item) {
      if(this.multiple) {
        let itemIndex = this.selected.findIndex(i => i.value === item.value)
        if(itemIndex === -1) {
          this.selected.push(item)
        } else {
          this.selected.splice(itemIndex, 1)
        }
        this.updateModel(this.selected)
      } else {
        this.selected = []
        if(!this.selected[0]) {
          this.selected[0] = item
        } else {
          this.selected = []
        }
        this.updateModel(item)
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
    },
    clearSelected() {
      this.selected = []
    }
  }
}
</script>
<style lang="scss">
$select-height : 30px;
$option-height : 40px;
$clear-btn-width: 40px;
$padding: .5rem;
$border-color: #c2c2c2;

.vue-tiny-select {
  position: relative;
  border: 1px solid $border-color;
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
  padding: $padding 50px $padding $padding;
  min-height: $select-height;
  align-items: baseline;
}
.vue-tiny-options {
  border: 1px solid $border-color;
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
  justify-content: flex-start;
  padding: 8px 16px;
  min-height: $option-height;
  border-bottom: 1px solid #eaeaea;
}
.vue-tiny-option:hover {
  background: #f4f2f2;
}
.vue-tiny-selected {
  color: white;
  padding-left: 8px;
  border-radius: 5px;
  display: flex;
  min-height: $select-height;
  align-items: center;
}
.vue-tiny-single-selected {
  padding-left: 8px;
  display: flex;
  align-items: center;
  min-height: $select-height;
}
.vue-tiny-close-btn {
  border-left: 1px solid white;
  margin-left: 8px;
  width: 24px;
}
.vue-tiny-close-btn:hover {
  color: #c4c4c4;
}
.caret-and-clear-btn {
  right: 10px;
  direction: rtl;
  top: $padding;
  width: $clear-btn-width;
  position: absolute;
  height: $select-height;
  display: flex;
  align-items: center;
}
.vue-tiny-clear-btn {
  color: #8d8d8d;
  font-size: 2rem;
}
.vue-tiny-clear-btn:hover {
  color: #464646;
}
.caret-down {
  width: 0;
  height: 0;
  margin-left: 8px;
  border-left: .5rem solid transparent;
  border-right: .5rem solid transparent;
  border-top: .5rem solid #656565;
  transform-origin: center;
  transition: .2s;
}
</style>