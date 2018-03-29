<template>
<div class="wrap">
  <silder-like>
    <silder-like-item v-for="(item, index) in items" :key="index">
      <h2>{{item.title}}</h2>
      <p>{{item.body}}</p>
    </silder-like-item>
  </silder-like>

  <div class="col">
    <button @click="addItem">增加一个item</button>
  </div>
</div>
</template>

<script>
import { SilderLike, SilderLikeItem } from '../src'

export default {
  name: 'demo',
  components: {
    SilderLike,
    SilderLikeItem
  },
  data () {
    return {
      items: [
        {title: '卡片1', body: '卡片1'},
        {title: '卡片2', body: '卡片2'},
        {title: '卡片3', body: '卡片3'}
      ]
    }
  },
  mounted () {
  },
  methods: {
    addItem () {
      this.items.push({title: '卡片' + (this.items.length + 1), body: '卡片' + (this.items.length + 1)},)
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
</style>