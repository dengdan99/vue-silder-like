<template>
  <div class="box">
    <div class="box-inr" :style="{width, height}">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'silder-like',
  data () {
    return {
      itemCount: 0
    }
  },
  props: {
    height: {
      type: String,
      default: '330px'
    },
    width: {
      type: String,
      default: '330px'
    },
    dragDistance: {
      type: Number,
      default: 100
    },
    baseIndex: {
      type: Number,
      default: 1000
    },
    topSpace: {
      type: Number,
      default: 40
    },
    showCardNumber: {
      type: Number,
      default: 3
    }
  },
  watch: {
    $children (val) {
      console.log(val)
    }
  },
  mounted () {
    // console.log(this.$children)
  },
  methods: {
    addCard (item) {
      this.itemCount ++
    },
    removeCard (item) {
      this.itemCount --
      this.$children.map((item, index) => item.init(index + 1))
    }
  }
}
</script>

<style lang="less" scoped>
.box{
  width: 100%;
  .box-inr{
    position: relative;
    margin: 0 auto;
  }
}
</style>
