<template>
  <div class="cartcontrol">
    <transition name="move">
      <div class="cart-decrease" v-show="food.count>0" @click.stop.prevent="decreaseCart">
        <span class="inner icon-remove_circle_outline"></span>
      </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.stop.prevent="addCart"></div>
  </div>
</template>

<script type="text/ecmascript-6">
  import Vue from 'vue';

  export default {
    props: {
      food: {
        type: Object
      }
    },
    created() {
    },
    methods: {
      addCart(event) {
        if (!this.food.count) {
          // 对此时的food对象没有count属性，只能添加一个使用Vue.set
          Vue.set(this.food, 'count', 1);
        } else {
          this.food.count++;
        }
        this.$emit('addcart', event.target);
      },
      decreaseCart() {
        if (this.food.count) {
          this.food.count--;
        }
      }
    }
  };
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size 0
    .cart-decrease
      display: inline-block
      padding: 6px
      transition: all 0.4s linear
      &.move-transition
        opacity: 1
        transform translate3d(0, 0, 0)
      .inner
        display inline-block
        font-size: 24px;
        line-height: 24px;
        color: rgb(0, 160, 220)
        transition all 0.4s linear
        transform rotate(0)
      &.move-enter, &.move-leave-active
        opacity 0
        transform translate3d(24px, 0, 0)
        .inner
          transform rotate(180deg)
    .cart-count
      display: inline-block
      vertical-align top
      font-size 10px
      width: 12px
      padding-top 6px
      line-height: 24px
      text-align: center
      color rgb(147, 153, 159)
    .cart-add
      display: inline-block;
      line-height: 24px;
      font-size: 24px;
      padding: 6px;
      color: rgb(0, 160, 220);
</style>
