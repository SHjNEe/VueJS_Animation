<template>
  <!-- <div>
    <div class="container">
      <user-list></user-list>
    </div>
    <div class="container">
      <div class="block" :class="{ animate: animatedBlock }"></div>
      <button @click="animateBlock">Animate</button>
    </div>
    <div class="container">
      <transition name="para">
        <p v-if="paraIsVisible">This is only some visible</p>
      </transition>
      <button @click="toggleParagraph">Toggle paragraph</button>
    </div>
    <div class="container">
      <transition
        :css="false"
        name="fade-button"
        mode="out-in"
        @before-enter="beforeEnter"
        @before-leave="beforeLeave"
        @enter="enter"
        @after-enter="afterEnter"
        @leave="leave"
        @after-leave="afterLeave"
        @enter-cancelled="enterCancelled"
        @leave-cancelled="leaveCancelled"
      >
        <button @click="showUser" v-if="!userIsVisible">Show User</button>
        <button @click="hideUser" v-else>Hide User</button>
      </transition>
    </div>
    <base-modal @close="hideDialog" :open="dialogIsVisible">
      <p>This is a test dialog!</p>
      <button @click="hideDialog">Close it!</button>
    </base-modal>
    <div class="container">
      <button @click="showDialog">Show Dialog</button>
    </div>
  </div> -->

  <!-- <transition name="route">
    <router-view></router-view>
  </transition> -->
  
  <router-view v-slot="slotProps">
    <transition name="fade-button" mode="out-in">
      <component :is="slotProps.Component"></component>
    </transition>
  </router-view>
</template>

<script>
import ListData from "./components/ListData.vue";
export default {
  // components: {
  //   userList: ListData,
  // },
  data() {
    return {
      dialogIsVisible: false,
      animatedBlock: false,
      paraIsVisible: false,
      userIsVisible: false,
    };
  },
  methods: {
    showDialog() {
      this.dialogIsVisible = true;
    },
    hideDialog() {
      this.dialogIsVisible = false;
    },
    animateBlock() {
      this.animatedBlock = true;
    },
    toggleParagraph() {
      this.paraIsVisible = !this.paraIsVisible;
    },
    showUser() {
      this.userIsVisible = true;
    },
    hideUser() {
      this.userIsVisible = false;
    },
    beforeEnter(el) {
      console.log(el);
      // console.log("Hi");
      el.style.opacity = 0;
    },
    beforeLeave(el) {
      console.log(el);
      el.style.opacity = 1;

      // console.log("Bye");
    },
    enter(el, done) {
      console.log("Enter");
      let round = 1;
      const interval = setInterval(function () {
        el.style.opacity = round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(interval);
          done();
        }
      }, 10);
    },
    afterEnter() {
      console.log("After enter");
    },
    leave(el, done) {
      console.log("Leave");
      let round = 1;
      const interval = setInterval(function () {
        el.style.opacity = 1 - round * 0.01;
        round++;
        if (round > 100) {
          clearInterval(interval);
          done();
        }
      }, 10);
    },
    afterLeave() {
      console.log("After Leave");
    },
    enterCancelled() {},
    leaveCancelled() {},
  },
};
</script>

<style>
* {
  box-sizing: border-box;
}
html {
  font-family: sans-serif;
}
body {
  margin: 0;
}
button {
  font: inherit;
  padding: 0.5rem 2rem;
  border: 1px solid #810032;
  border-radius: 30px;
  background-color: #810032;
  color: white;
  cursor: pointer;
}
button:hover,
button:active {
  background-color: #a80b48;
  border-color: #a80b48;
}
.block {
  width: 8rem;
  height: 8rem;
  background-color: #290033;
  margin-bottom: 2rem;
  /* transition: 2s; */
}
.container {
  max-width: 40rem;
  margin: 2rem auto;
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
  padding: 2rem;
  border: 2px solid #ccc;
  border-radius: 12px;
}
.animate {
  /* transform: translateX(-150px); */
  animation: slide-fade 0.3s forwards;
}
.para-enter-from {
  opacity: 0;
  transform: translateY(-30px);
}

.para-enter-active {
  transition: all 0.6s ease-out;
}

.para-enter-to {
  opacity: 1;
  transform: translateY(0);
}

.para-leave-from {
  opacity: 1;
  transform: translateY(0);
}

.para-leave-active {
  transition: all 0.6s ease-out;
}

.para-leave-to {
  opacity: 0;
  transform: translateY(-30px);
}
.fade-button-enter-from,
.fade-button-leave-to {
  opacity: 0;
}
.fade-button-enter-active {
  transition: opacity 1s;
}
.fade-button-leave-active {
  transition: opacity 1s;
}
.fade-button-enter-to,
.fade-button-leave-from {
  opacity: 1;
}

.route-enter-from {
}
.route-enter-active {
  animation: slide-scale 0.5s;
}
.route-enter-to {
}

.route-leave-active {
  animation: slide-scale 0.5s;
}
@keyframes slide-scale {
  0% {
    transform: translateX(0) scale(1);
  }
  70% {
    transform: translateX(-60px) scale(1.1);
  }
  100% {
    transform: translateX(-150px) scale(1);
  }
}
</style>
