<template>
  <div class="slider">
    <transition-group tag="div" :name="transitionName" class="slides-group">
      <div v-if="show" :key="current" class="slide" :class="slides[current].className">
        <p>I'm {{slides[current].className}}!</p>
      </div>
    </transition-group>
    <div class="btn btn-prev" aria-label="Previous slide" @click="slide(-1)">
      &#10094;
    </div>
    <div class="btn btn-next" aria-label="Next slide" @click="slide(1)">
      &#10095;
    </div>
  </div>
</template>

<script>
export default {
  name: "CarouselComponent",
  data() {
    return {
      current: 0,
      direction: 1,
      transitionName: "fade",
      show: false,
      slides: [
        {className: "blue"},
        {className: "red"},
        {className: "yellow"}
      ]
    }
  },
  mounted() {
    this.show = true;
  },
  methods: {
    slide(direction) {
      this.direction = direction;
      direction === 1 ? (this.transitionName = "slide-next") : (this.transitionName = "slide-prev");
      let len = this.slides.length;
      this.current = (this.current + direction % len + len) % len;
      }
    },

}
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css?family=Crimson+Text");
.fade-enter-active {
  transition: opacity 1s;
}
.fade-enter {
  opacity: 0;
}
.slide-next-enter-active,
.slide-next-leave-active {
  transition: transform 0.5s ease-in-out;
}
.slide-next-enter {
  transform: translate(100%);
}
.slide-next-leave-to {
  transform: translate(-100%);
}

.slide-prev-enter-active,
.slide-prev-leave-active {
  transition: transform 0.5s ease-in-out;
}
.slide-prev-enter {
  transform: translate(-100%);
}
.slide-prev-leave-to {
  transform: translate(100%);
}

.blue {
  background: #4a69bd;
}
.red {
  background: #e55039;
}

.yellow {
  background: #f6b93b;
}

.slider {
  width: 60%;
  height: 60vh;
  overflow: hidden;
  margin: 0;
  font-size: 50px;
  font-family: "Crimson Text", sans-serif;
  color: #fff;
}

.slide {
  width: 100%;
  height: 100vh;
  position: absolute;
  top: 0;
  left: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn {
  z-index: 10;
  cursor: pointer;
  border: 3px solid #fff;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 70px;
  height: 70px;
  position: absolute;
  top: calc(50% - 35px);
  left: 1%;
  transition: transform 0.3s ease-in-out;
  user-select: none;
}

.btn-next {
  left: auto;
  right: 1%;
}

.btn:hover {
  transform: scale(1.1);
}




</style>