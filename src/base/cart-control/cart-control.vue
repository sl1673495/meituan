<template>
  <div class="cart-control">
    <transition name="move">
      <div
        @click.stop="decrease"
        class="cart-decrease"
        v-show="food.number"
      >
        <span class="inner icon-sell-remove_circle_outline"></span>
      </div>
    </transition>
    <div
      class="number"
      v-show="food.number"
    >{{food.number}}</div>
    <div
      @click.stop="add"
      class="cart-add"
    >
      <span class="inner icon-sell-add_circle"></span>
    </div>
  </div>
</template>

<script>
import { ballToElement } from "@/common/js/dom"
export default {
  props: {
    food: {
      type: Object,
      default() {
        return {}
      }
    },
    // 小球动画需要飞到的目标
    target: {
      type: HTMLDivElement,
      default: null
    }
  },
  created() {},
  methods: {
    add(e) {
      if (this.target) {
        ballToElement(e, this.target)
      }
      if (!this.food.number) {
        this.$set(this.food, "number", 1)
        return
      }
      this.food.number++
    },
    decrease() {
      this.food.number--
    }
  },
  data() {
    return {}
  }
}
</script>

<style lang="stylus" scoped>
@import '~common/stylus/variable.styl';

.cart-control {
  font-size: 1rem;

  .cart-decrease, .cart-add, .number {
    display: inline-block;
    vertical-align: middle;
    font-size: $font-size-small;
    color: $color-text-grey;
    opacity: 1;
    transform: translate3d(0, 0, 0);

    .inner {
      display: inline-block;
      transition: all 0.4s linear;
      transform: rotate(0);
    }

    &.move-enter-active, &.move-leave-active {
      transition: all 0.4s linear;
    }

    &.move-enter, &.move-leave-active {
      opacity: 0;
      transform: translate3d(24px, 0, 0);

      .inner {
        transform: rotate(180deg);
      }
    }

    span {
      font-size: 1.7rem;
      color: #FFD161;
    }
  }

  .cart-decrease, .number {
    margin-right: 0.5rem;
  }
}
</style>
