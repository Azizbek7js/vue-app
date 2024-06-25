<template>
  <div class="d-flex gap-4">
    <div class="slider">
      <transition-group tag="div" :name="transitionName" class="slides-group">
        <div v-if="show" :key="current" class="slide" :style="{backgroundColor: slides[current].className}" >
          <p>{{slides[current].className}}</p>
        </div>
      </transition-group>
      <button class="btn btn-prev" aria-label="Previous slide" @click="slide(-1)">
        &#10094;
      </button>
      <div class="btn btn-next" aria-label="Next slide" @click="slide(1)">
        &#10095;
      </div>
      <div class="bottom-toggleBtn">
        <div v-for="(slide , index ) in slides" :key="slide" class="btn-slide" @click="changeCurrent(index)">
          <div v-if="index === current" class="btn-active"></div>
        </div>
      </div>
    </div>
    <div>
       <div class="d-flex align-items-center gap-2">
         <input type="checkbox" v-model="autoChange">
         <input type="number" v-model="autoChangeTime">
         <span>auto</span>
       </div>
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
      autoChange:false,
      autoChangeTime: 1,
      intervalId: null,
      slides: [
        {className: "blue"},
        {className: "red"},
        {className: "yellow"},
        {className: "black"},
        {className: "green"},
        {className: "pink"},
      ]
    }
  },
  mounted() {
    this.show = true;
  },
  watch:{
    autoChange(val){
      if(val){
        this.intervalId = setInterval(()=>{
          this.slide(1)
        }, this.autoChangeTime*1000)
      }else{
        clearInterval(this.intervalId)
        this.intervalId =null
      }
    },
  },
  methods: {
    slide(direction) {
      this.direction = direction;
      direction === 1 ? (this.transitionName = "slide-next") : (this.transitionName = "slide-prev");
      let len = this.slides.length;
      this.current = (this.current + direction % len + len) % len;
    },
    changeCurrent(direction){
      this.current < direction ? (this.transitionName = "slide-next") : (this.transitionName = "slide-prev");
      this.current = direction
    }
  },
}
</script>

<style scoped>
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
  width: 600px;
  height: 600px;
  overflow: hidden;
  margin: 0;
  position: relative;
  font-size: 50px;
  color: #fff;
}
.bottom-toggleBtn{
  position: absolute;
  width: 100%;
  padding: 10px 0 ;
  bottom: 0;
  z-index: 11;
  display: flex;
  font-size: 20px;
  justify-content: center;
  gap: 30px;
  background-color: rgba(0, 0, 0, 0.5);
}
.btn-slide{
  display: flex;
  align-items: center;
  justify-content: center;
  width: 20px;
  height: 20px;
  background-color: rgba(218, 218, 218, 0.65);
  border-radius: 100%;
}
.btn-active{
  width: 10px;
  height: 10px;
  border-radius: 100%;
  background-color: #ffff
}
.slide {
  width: 100%;
  height: 100vh;
  position: absolute;
  display: flex;
  align-items: center;
  justify-content: center;
}

.btn {
  z-index: 10;
  cursor: pointer;
  display: flex;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  border-radius: 100%;
  background-color: #37474F;
  position: absolute;
  top: 250px;
  left: 1%;
  font-size: large;
  transition: transform 0.3s ease-in-out;
  user-select: none;
  border: none;
}

.btn-next {
  left: auto;
  right: 1%;
}






</style>