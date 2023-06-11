<template>
  <div class="container mx-auto py-20">
    <h2 class="text-3xl font-medium tracking-tight text-gray-900">Section Title</h2>

    <div class="mt-10" @mousedown.left="onMouseDown">
      <VueHorizontal responsive class="horizontal" ref="horizontal" snap="none" :button="false" @scroll="onScroll">
        <div class="relative mx-3" v-for="i in Array(999).keys()" :key="i">
          <button class="group" type="button" @click="relocate">
            <div class="w-full overflow-hidden rounded-md bg-gray-200 hover:opacity-75 hover:scale-150 lg:h-80">
              <img src="https://tailwindui.com/img/ecommerce-images/product-page-01-related-product-01.jpg" class="h-full w-full object-cover object-center lg:h-full lg:w-full group-hover:scale-125 ease-in duration-150">
            </div>

            <div class="mt-4 flex justify-between">
              <div>
                <h3 class="text-sm text-gray-700">
                  <span aria-hidden="true" class="absolute inset-0"></span>
                  <span>Basic Tee (${{ i }})</span>
                </h3>
              </div>
            </div>

            <div class="opacity-0 group-hover:opacity-100 absolute bottom-10 right-0 bg-white shadow rounded-full h-10 w-10 flex items-center justify-center">
              <svg xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke-width="1.5" stroke="currentColor" class="w-6 h-6">
                <path stroke-linecap="round" stroke-linejoin="round" d="M13.5 4.5L21 12m0 0l-7.5 7.5M21 12H3" />
              </svg>
            </div>
          </button>
        </div>
      </VueHorizontal>
    </div>
  </div>
</template>

<script>
import VueHorizontal from 'vue-horizontal';
import Placeholder from './components/Placeholder.vue';

export default {
  components: {
    VueHorizontal,
    Placeholder
  },

  data () {
    return {
      left: 0,
      originX: 0,
      originLeft: 0,
    };
  },
  destroyed () {
    this.onMouseUp();
  },
  methods: {
    relocate () {
      window.location.href = '/';
    },

    onScroll ({ left }) {
      this.left = left;
    },
    onMouseDown (e) {
      this.originX = e.pageX;
      this.originLeft = this.left;

      window.addEventListener("mouseup", this.onMouseUp);
      window.addEventListener("mousemove", this.onMouseMove);
    },
    onMouseUp () {
      window.removeEventListener("mouseup", this.onMouseUp);
      window.removeEventListener("mousemove", this.onMouseMove);
    },
    onMouseMove (e) {
      const offset = e.pageX - this.originX;
      const left = this.originLeft - offset;
      this.$refs.horizontal.scrollToLeft(left, 'auto');
    }
  }
};
</script>

<style scoped>
.horizontal {
  cursor: move;
  user-select: none;
}
</style>
