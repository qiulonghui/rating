<template>
  <div class="rating">

    <symbol id="icon-star-full" viewBox="0 0 1024 1024">
      <path d="M964.608 424.96L752.64 631.808l50.176 290.816c1.024 8.192-2.048 15.36-8.192 20.48-3.072 3.072-8.192 4.096-12.288 4.096-3.072 0-6.144-1.024-9.216-2.048L512 806.912 250.88 944.128c-7.168 4.096-15.36 3.072-21.504-2.048-6.144-4.096-9.216-12.288-8.192-20.48l50.176-290.816L59.392 424.96c-5.12-5.12-7.168-13.312-5.12-21.504 2.048-7.168 9.216-13.312 16.384-14.336l291.84-40.96L493.568 82.944c3.072-7.168 10.24-11.264 18.432-11.264s15.36 4.096 18.432 11.264L661.504 348.16l291.84 41.984c8.192 1.024 14.336 6.144 16.384 14.336s0 15.36-5.12 20.48z" p-id="1364"></path>
    </symbol>

    <div class="star-wrap" v-for="n in count" :key="n" @mouseover="onOver(n)" @mouseout="onOut" @click="setScore(n)">
      <div class="mask" v-show="n <= Math.ceil(curScore)" :style="{
          width: (curScore - n < 0 ? (1 + curScore - n) * 100 : 100) + '%',
        }">
        <img class="img" v-if="activeImage" :src="activeImage" :style="customImgStyle">
        <svg v-else class="icon" :style="{fill:activeColor}" :width="size" :height="size">
          <use :xlink:href="'#'+iconid"></use>
        </svg>
      </div>
      <img class="img" v-if="inactiveImage" :src="inactiveImage" :style="customImgStyle">
      <svg v-else class="icon" :style="{fill:inactiveColor}" :width="size" :height="size">
        <use :xlink:href="'#'+iconid"></use>
      </svg>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Rating',
  components: {},
  props: {
    value: {
      type: [Number, String],
      default: 0
    },
    count: {
      type: Number,
      default: 6
    },
    size: {
      type: String,
      default: '40'
    },
    disabled: {
      type: Boolean,
      default: false
    },
    iconid: {
      type: String,
      default: 'icon-star-full'
    },
    activeColor: {
      type: String,
      default: '#1500b0'
    },
    inactiveColor: {
      type: String,
      default: '#7669d6'
    },
    activeImage: {
      type: String,
      default: ''
    },
    inactiveImage: {
      type: String,
      default: ''
    },
    customImgStyle: Object
  },
  data() {
    return {
      curScore: this.value
    }
  },
  computed: {},
  created() {},
  methods: {
    onOver(n) {
      if (n < this.value) return
      if (!this.disabled) this.curScore = n
    },
    onOut() {
      if (!this.disabled) this.curScore = this.value
    },
    setScore(n) {
      if (this.disabled) return
      this.$emit('input', n)
      this.$emit('after-rate', n)
    }
  }
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
  .img {
    width: 40px;
    height: 40px;
  }
}
</style>
