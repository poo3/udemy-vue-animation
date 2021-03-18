<template>
  <div class="main">
    <button @click="myAnimation = 'slide'">slide</button>
    <button @click="myAnimation = 'fade'">fade</button>
    <p>{{ myAnimation }}</p>
    <button @click="show = !show">切り替え</button>
    <br /><br />
    <transition
      :css="false"
      @enter="enter"
      @leave="leave"
      @before-enter="beforeEnter"
    >
      <div class="circle" v-if="show"></div>
    </transition>
    <transition :name="myAnimation" appear>
      <p v-if="show">hello</p>
    </transition>
    <transition name="slide" type="animation">
      <p v-if="show">bye</p>
    </transition>
    <transition
      appear
      enter-active-class="animate__animated animate__rubberBand"
      leave-active-class="animate__animated animate__backOutRight"
    >
      <p v-if="show">Animation.css</p>
    </transition>
    <transition name="fade" mode="out-in">
      <p v-if="show" key="hello">こんにちは！</p>
      <p v-else key="bye">さようなら〜</p>
    </transition>
    <button @click="myComponent = 'ComponentA'">ComponentA</button>
    <button @click="myComponent = 'ComponentB'">ComponentB</button>
    <br />
    <transition name="fade" mode="out-in">
      <component :is="myComponent"></component>
    </transition>
    <br /><br />
    <button @click="addNumber">addNum</button>
    <ul class="number-list">
      <li v-for="number in numbers" :key="number" @click="removeNum">{{ number }}</li>
    </ul>
  </div>
</template>

<script>
import ComponentA from "./components/ComponentA";
import ComponentB from "./components/ComponentB";
export default {
  components: {
    ComponentA,
    ComponentB,
  },
  data() {
    return {
      show: true,
      myAnimation: "slide",
      myComponent: "ComponentA",
      numbers: [0, 1, 2, 3],
      nextNum: 4,
    };
  },
  methods: {
    removeNum(){
      this.numbers.splice(this.number,1)
    },
    randomNum() {
      return Math.floor(Math.random() * this.numbers.length);
    },
    addNumber() {
      this.numbers.splice(this.randomNum(), 0, this.nextNum);
      this.nextNum += 1;
    },
    beforeEnter(el) {
      el.style.transform = `scale(0)`;
    },
    enter(el, done) {
      let scale = 0;
      const interval = setInterval(() => {
        el.style.transform = `scale(${scale})`;
        scale += 0.1;
        if (scale > 1) {
          clearInterval(interval);
          done();
        }
      }, 30);
    },
    leave(el, done) {
      let scale = 1;
      const interval = setInterval(() => {
        el.style.transform = `scale(${scale})`;
        scale -= 0.1;
        if (scale < 0) {
          clearInterval(interval);
          done();
        }
      }, 30);
    },
  },
};
</script>

<style scoped>
.number-list {
  width: 300px;
  margin: auto;
}
.circle {
  width: 200px;
  height: 200px;
  margin: auto;
  background-color: aquamarine;
  border-radius: 100px;
}
.fade-enter {
  opacity: 0;
}
.fade-enter-to {
  opacity: 1;
}
.fade-enter-active {
  transition: opacity 1s;
}
.fade-leave {
  opacity: 1;
}
.fade-leave-to {
  opacity: 0;
}
.fade-leave-active {
  transition: opacity 1s;
}

.main {
  text-align: center;
  margin: 0 auto;
  padding-top: 5rem;
}

.slide-enter,
.slide-leave-to {
  opacity: 0;
}

.slide-enter-active {
  animation: slide-in 1s;
  transition: 2s;
}
.slide-leave-active {
  animation: slide-in 1s reverse;
  transition: 2s;
}

@keyframes slide-in {
  from {
    transform: translateX(100px);
  }
  to {
    transform: translateX(0);
  }
}
</style>
