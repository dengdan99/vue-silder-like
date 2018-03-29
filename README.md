# vue-silder-like

> A Vue component

> 模仿探探，左滑喜欢， 右滑不喜欢
## [Live demo](https://dengdan99.github.io/vue-silder-like/)

## Installation

### NPM
```bash
$ npm install vue-silder-like
```

### ES6
```js
import { SilderLike, SilderLikeItem } from 'vue-silder-like'

new Vue({
  components: {
    SilderLike,
    SilderLikeItem
  }
})
```


### .vue
```html
<template>
<div class="wrap">
  <div class="box">
    <silder-like 
      :drag-distance="150" 
      :top-space="30" 
      :show-card-number="4"
      height="330px" 
      width="330px">
      <silder-like-item 
        @silder-left="like(item)" 
        @silder-right="nulike(item)" 
        v-for="(item, index) in items" 
        :key="index">
        <h2>{{item.title}}</h2>
        <p>{{item.body}}</p>
        <img :src="item.img" />
      </silder-like-item>
    </silder-like>
  </div>

  <div class="col">
    <button @click="addItem">增加一个item</button>
  </div>
</div>
</template>

<script>
import { SilderLike, SilderLikeItem } from 'vue-silder-like'

export default {
  name: 'demo',
  components: {
    SilderLike,
    SilderLikeItem
  },
  data () {
    return {
      items: [
        {title: '卡片1', body: '内容1', img: '//static.51kcwc.com/car/static/activity/spring/zunyi/h1@2x.png'},
        {title: '卡片2', body: '内容2', img: '//static.51kcwc.com/car/static/activity/spring/zunyi/h1@2x.png'},
        {title: '卡片3', body: '内容3', img: '//static.51kcwc.com/car/static/activity/spring/zunyi/h1@2x.png'}
      ]
    }
  },
  mounted () {
  },
  methods: {
    addItem () {
      this.items.push({title: '卡片' + (this.items.length + 1), body: '卡片' + (this.items.length + 1), img: '//static.51kcwc.com/car/static/activity/spring/zunyi/h1@2x.png'})
    },
    nulike (item) {
      console.log('不喜欢', item)
    },
    like (item) {
      console.log('喜欢', item)
    }
  }
}
</script>

<style lang="less">
html{
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  font-size: 14px;
}
html,body {
  padding: 0;
  margin: 0;
}
.wrap{
  margin-top: 45px;
}
.box{
  padding-bottom: 50px;
}
</style>
```

## 选项
silder-like 属性
1. `drag-distance`：Number 拖动触发行为的距离
2. `top-space`：Number 每个卡片的显示距离（用top来控制）
3. `show-card-number`：Number 显示的卡片数量
4. `height`：String 卡片的高度
5. `width`：String 卡片的宽度

silder-like-item 方法
1. `@silder-left` 向左滑动
2. `@silder-right` 向右滑动