<template>
  <div class="main">
    <button @click="show = !show">切り替え</button>
    <transition name="fade">
      <p v-if="show">hello</p>
    </transition>
    <transition name="slide" type="animation">
      <p v-if="show">bye</p>
    </transition>
    <transition
      appear
      enter-active-class = "animate__animated animate__rubberBand"
      leave-active-class = "animate__animated animate__backOutRight"
    >
      <p v-if="show">Animation.css</p>
    </transition>
  </div>
</template>

<script>
export default {
  data() {
    return {
      show: true,
    };
  },
};
</script>

<style>
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

.slide-enter,.slide-leave-to{
  opacity: 0;
}

.slide-enter-active {
  animation: slide-in 1s;
  transition: 2s;
}
.slide-leave-active {
  animation: slide-in 1s reverse;
  transition:2s;
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
