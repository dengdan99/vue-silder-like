<template>
  <div class="box">
    <div class="box-inr">
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: 'silder-like',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App',
      itemCount: 0
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
      this.$children.map((item, index) => item.initCardStyle(index + 1))
    }
  }
}
</script>

<style lang="less" scoped>
.box{
  width: 100%;
  height: 480px;
  background-color: #cfcfcf;
  .box-inr{
    position: relative;
    margin: 0 auto;
    height: 330px;
    width: 330px;
  }
}
</style>
