# vue-silder-like

> A Vue component

> 模仿探探，左滑喜欢， 右滑不喜欢

## [Live demo](https://dengdan99.github.io/vue-comparison/example-dist/)

## Installation

### NPM
```bash
$ npm install vue-silder-like
```

### CommonJS
```js
var comparison = require('vue-comparison/src/Comparison.vue');

new Vue({
  components: {
    'comparison': comparison
  }
})
```

### ES6
```js
import { Comparison } from 'vue-silder-like'

new Vue({
  components: {
    Comparison
  }
})
```
### 
```html
<comparison
  :data = "mockData"
  :contrast = "contrast"
  :props = "compProps"
  @add-item = "addItemHander"
  >
    <div slot="symbol">
      <span class="tp-icon">- 无</span>
      <span class="tp-icon">* 选配</span>
      <span class="tp-icon">+ 标配</span>
    </div>
  </comparison>
```