
 <img src="https://github.com/return75/return75/raw/main/gifs/vue-tiny-select.gif" />
<br>
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
import "vue-tiny-select/dist/vue-tiny-select.css"

export default {
  name: 'App',
  components: {
    VueTinySelect
  },
  data() {
    return {
      selected: null,
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
    }
  },
}
```

