<template>
  <div class="card" :class="{touched: isTouch}" :style="cardStyle" v-show="isShow">
    <slot></slot>
  </div>
</template>

<script>
export default {
  name: 'silder-like-item',
  props: {
    extData: [Number, String, Object]
  },
  data () {
    return {
      isTouch: false,
      cardStyle: {
        left: 0,
        top: 0,
        width: '0',
        height: '0',
        transform: 'scale(1)',
        transition: 'all 0.5s',
        'z-index': 0,
        opacity: 1
      },
      isSurface: false,
      isShow: true,
      sPos: {y: 0, x: 0},
      mPos: {y: 0, x: 0},
      ePos: {y: 0, x: 0}
    }
  },
  computed: {
    dragDistance () {
      return this.$parent.dragDistance
    },
    baseIndex () {
      return this.$parent.baseIndex
    },
    topSpace () {
      return this.$parent.topSpace
    },
    showCardNumber () {
      return this.$parent.showCardNumber
    }
  },
  created () {
    this.cardStyle.width = this.$parent.width
    this.cardStyle.height = this.$parent.height
  },
  mounted () {
    this.$parent.addCard(this)
    this.init()
  },
  methods: {
    init (index) {
      this.initCardStyle(index)
      if (index === 1 || this.$parent.itemCount === 1) {
        this.isSurface = true
        this.dragInit()
      }
    },
    initCardStyle (index) {
      const _i = index || this.$parent.itemCount
      if (_i <= this.showCardNumber) {
        this.isShow = true
        this.cardStyle.top = ((_i - 1) * this.topSpace) + 'px'
        this.cardStyle.transform = 'scale(' + (11 - _i) / 10 + ')'
        this.cardStyle['z-index'] = this.baseIndex - _i
      } else {
        this.isShow = false
      }
    },
    dragInit () {
      const $el = this.$el
      $el.addEventListener('touchstart', this.touchStart, false)
      $el.addEventListener('touchmove', this.touchMove, false)
      $el.addEventListener('touchend', this.touchEnd, false)
    },
    touchStart () {
      this.isTouch = true
      this.cardStyle.transition = 'none'
      const touch = event.touches[0]
      this.sPos.y = touch.pageY
      this.sPos.x = touch.pageX
    },
    touchMove () {
      const touch = event.touches[0]
      this.mPos.x = touch.pageX
      this.mPos.y = touch.pageY
      const disX = this.mPos.x - this.sPos.x
      const disY = this.mPos.y - this.sPos.y
      let rotate = 0
      if (disX > 0) {
        rotate = rotate > 3 ? rotate : disX * 0.05
      } else {
        rotate = rotate < -3 ? rotate : disX * 0.05
      }
      this.cardStyle.transform = 'scale(1) rotate(' + rotate + 'deg)'
      this.cardStyle.left = disX + 'px'
      this.cardStyle.top = disY + 'px'
    },
    touchEnd () {
      this.isTouch = false
      this.cardStyle.transition = 'all 0.5s'
      this.cardStyle.transform = this.cardStyle.transform.split(' ')[0] || 'scale(1)'
      if (parseInt(this.cardStyle.left) < -this.dragDistance) {
        this.cardStyle.opacity = 0
        this.silderToLeft()
      } else if (parseInt(this.cardStyle.left) > this.dragDistance) {
        this.cardStyle.opacity = 0
        this.silderToRight()
      } else {
        this.cardStyle.left = '0px'
        this.cardStyle.top = '0px'
      }
    },
    silderToLeft () {
      this.$emit('silder-left')
      this.deleteItem()
    },
    silderToRight () {
      this.$emit('silder-right')
      this.deleteItem()
    },
    deleteItem () {
      this.$destroy(true)
    }
  },
  destroyed () {
    if (this.$el && this.$el.parentNode) {
      this.$el.parentNode.removeChild(this.$el)
    }
    this.$parent.removeCard(this)
  }
}
</script>

<style lang="less" scoped>
.card{
  position: absolute;
  background-color: #fff;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.2);
  border-radius: 5px;
  overflow: hidden;
  &.touched{
  }
}
</style>
