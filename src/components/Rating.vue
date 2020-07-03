<template>
  <div class="rating">
    <div
      class="star-wrap"
      v-for="n in count"
      :key="n"
      @mouseenter="disabled ? null : (curScore = n)"
      @click="setScore(n)"
    >
      <div
        class="mask"
        v-show="n <= Math.ceil(curScore)"
        :style="{
          width: (curScore - n < 0 ? (1 + curScore - n) * 100 : 100) + '%',
        }"
      >
        <Star :size="size" color="#f2b50f" />
      </div>
      <Star :size="size" class="b-shape" />
    </div>
  </div>
</template>

<script>
import Star from './Star'

export default {
  name: 'Rating',
  components: {
    Star,
  },
  props: {
    score: {
      type: Number,
      default: 1.8,
    },
    count: {
      type: Number,
      default: 6,
    },
    size: {
      type: String,
      default: '40',
    },
    disabled: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      curScore: this.score,
    }
  },
  computed: {},
  created() {},
  methods: {
    setScore(n) {
      console.log(1)
      this.curScore = n
    },
  },
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.rating {
  display: flex;
  justify-content: center;
  .star-wrap {
    position: relative;
  }
  .mask {
    position: absolute;
    top: 0;
    left: 0;
    z-index: 1;
    overflow: hidden;
  }
}
</style>
