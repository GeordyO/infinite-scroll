<template>
  <div>
    <div class="container relative block lg:flex justify-between">
      <div>
        <h1 class="font-bold text-gray-500 mb-1">eyebrow</h1>
        <h4 class="font-extrabold leading-none">Main title</h4>
      </div>
      <div class="absolute right-0 bottom-0 hidden xl:flex space-x-2 mt-2">
        <div
          class="transition-all ease-in-out duration-200 hidden lg:flex items-center justify-center bg-gray-200 dark:bg-black hover:bg-black dark-hover:bg-white hover:text-white dark-hover:text-black rounded-full h-8 w-8 cursor-pointer"
          @click="move('left')"
        ></div>
        <div
          class="transition-all ease-in-out duration-200 hidden lg:flex items-center justify-center bg-gray-200 dark:bg-black hover:bg-black dark-hover:bg-white hover:text-white dark-hover:text-black rounded-full h-8 w-8 cursor-pointer"
          @click="move('right')"
        ></div>
      </div>
    </div>
    <div class="carousel-container relative mx-auto overflow-x-hidden h-full">
      <div
        ref="hor-scroll"
        class="hide-scroll transition-all duration-500 ease-in-out absolute flex top-0 left-0 overflow-x-scroll space-x-8"
      >
        <slot name="scrollItem"></slot>
        <slot name="scrollItem"></slot>
        <slot name="scrollItem"></slot>
        <slot name="scrollItem"></slot>
        <slot name="scrollItem"></slot>
      </div>
      <div class="left-gradient"></div>
      <div class="right-gradient"></div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      transformLeft: 0,
      cardAmount: null,
      initCardMove: 0,
    }
  },

  computed: {
    totalCards() {
      return this.$refs['hor-scroll'].children.length
    },
  },
  beforeMount() {},
  mounted() {
    this.baseCards()
    console.log(this.$slots)
    this.initCardMove = this.cardAmount * 2 - 1
    this.transformLeft =
      -250 - 364 * this.initCardMove - 32 * (this.cardAmount * 2)
    for (const item of this.$refs['hor-scroll'].children) {
      item.style.transform = `translateX(${this.transformLeft}px)`
    }
  },
  methods: {
    move(direction) {
      //   const moveAmount =
      //     this.$refs['hor-scroll'].children[0].getBoundingClientRect().width + 32
      //   this.transformLeft =
      //     direction === 'left'
      //       ? this.transformLeft + moveAmount
      //       : this.transformLeft - moveAmount
      //   for (const item of this.$refs['hor-scroll'].children) {
      //     item.style.transform = `translateX(${this.transformLeft}px)`
      //   }
      if (direction === 'left') {
        this.$refs['hor-scroll'].insertBefore(
          this.$refs['hor-scroll'].children[this.totalCards - 1],
          this.$refs['hor-scroll'].children[0]
        )
      } else {
        this.insertAfter(
          this.$refs['hor-scroll'].children[0],
          this.$refs['hor-scroll'].children[this.totalCards - 1]
        )
      }
    },

    insertAfter(newNode, referenceNode) {
      referenceNode.parentNode.insertBefore(newNode, referenceNode.nextSibling)
    },

    baseCards() {
      this.cardAmount = this.$slots.scrollItem.length
    },
  },
}
</script>
// 114px overflow on sides - slide over -290px for centering of 3 cards in
middle for desktop
<style lang="scss" scoped>
.carousel-container {
  margin-top: 20px;
  height: 483px;
  max-width: 1080px;

  @media screen and (min-width: 1440px) {
    max-width: 1384px;
  }
}

.scroll-items {
  @apply px-5;

  @media screen and (min-width: 640px) {
    @apply px-10;
  }

  @media screen and (min-width: 1024px) {
    @apply px-0;
  }
}

/* Hide scrollbar for IE, Edge and Firefox */
.hide-scroll {
  -ms-overflow-style: none; /* IE and Edge */
  scrollbar-width: none; /* Firefox */
  scroll-behavior: smooth;
}

/* Hide scrollbar for Chrome, Safari and Opera */
.hide-scroll::-webkit-scrollbar {
  display: none;
}

.dots {
  height: 72px;
  width: 72px;
  bottom: -32px;
  left: -28px;
}

.left-gradient,
.right-gradient {
  position: absolute;
  top: 0;
  height: 100%;
  width: 114px;
}

.left-gradient {
  left: 0;
  background-image: linear-gradient(to left, #eef1f400 0%, #eef1f4 70%);
}

.right-gradient {
  right: 0;
  background-image: linear-gradient(to right, #eef1f400 0%, #eef1f4 70%);
}
</style>
