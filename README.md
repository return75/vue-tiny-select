# vue-tiny-select

## installation
```
 npm install vue-tiny-select
```

### usage:
```
  <vue-tiny-select v-model="selected" :options="options" multiple></vue-tiny-select>
```
.vue file:
```
import VueTinySelect from "vue-tiny-select";
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
}
```
<br>
 <img src="https://github.com/return75/return75/raw/main/gifs/vue-tiny-select.gif" />
