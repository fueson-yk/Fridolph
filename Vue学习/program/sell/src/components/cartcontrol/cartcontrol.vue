<template>
  <div class="cartcontrol">
    <div 
      class="cart-decrease" 
      v-show="food.count > 0" 
      @click.stop.prevent="decreaseCart" 
      transition="move"
    >
      <span class="inner icon-remove_circle_outline"></span>
    </div>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
  </div>
</template>

<script tyep="text/ecmascript-6">
  import Vue from 'vue'

  export default {
    props: {
      food: {
        count: 0
      },
    },
    created() {
      // console.log(this.food)
    },
    methods: {
      addCart(e) {
        if (!e._constructed) {
          return
        }
        console.log('click')
        if (!this.food.count) {
          Vue.set(this.food, 'count', 1)
        } else {
          this.food.count++
        }
        this.$dispatch('cart.add', e.target)
      },
      decreaseCart(e) {
        if (!e._constructed) {
          return
        }
        if (this.food.count) {
          this.food.count--
        }
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 5px
      transition: all 0.4s linear
      &.move-transition
        opacity: 1
        transform: translate3d(0,0,0)
        .inner
          display: inline-block
          line-height: 20px
          font-size: 20px
          color: rgb(0,160,220)
          transition: all 0.4s linear
          transform: rotate(0)
      &.move-enter, &.move-leave
        opacity: 0
        transform: translate3d(24px,0,0)
        .inner
          transform: rotate(360deg)
    .cart-count
      display: inline-block
      position: relative
      top: -4px
      vertical-align: center
      width: 12px
      padding-top: 5px
      line-height: 20px
      text-align: center
      font-size: 10px
      color: rgb(147,153,159)
    .cart-add
      display: inline-block
      padding: 5px
      line-height: 20px
      font-size: 20px
      color: rgb(0,160,220)
</style>