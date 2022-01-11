<template>
  <button type="button" @click="flag = !flag">Toggle</button>
  <!-- 1. Animating with CSS transitions -->
  <!-- "mode" set to "in-out" by default -->
  <!-- <transition name="fade" mode="out-in">
    <h2 v-if="flag" key="main">Hello world!</h2>
    <h2 v-else key="secondary">Another hello!</h2>
  </transition> -->

  <!-- 2. Animating with CSS animations -->
  <!-- <transition name="zoom" appear>
    <h2 v-if="flag">Hello</h2>
  </transition> -->

  <!-- 3. Animations with JS -->
  <!--     @before-enter="beforeEnter"
    @after-enter="afterEnter"
    @before-leave="beforeLeave"
    @after-leave="afterLeave" -->
  <transition @enter="enter" @leave="leave" :css="false">
    <h2 v-if="flag">Hey</h2>
  </transition>

  <p></p>
</template>

<script>
export default {
  name: "App",
  data() {
    return {
      flag: false,
    };
  },
  methods: {
    // 3. Animations with JS
    beforeEnter(el) {
      console.log("before enter", el);
    },
    enter(el, done) {
      const animation = el.animate([{ transform: "scale3d(0,0,0)" }, {}], {
        duration: 1000,
      });
      animation.onfinish = () => {
        done();
      };

      console.log("enter", el);
      done();
    },
    afterEnter(el) {
      console.log("after enter", el);
    },
    beforeLeave(el) {
      console.log("before leave", el);
    },
    leave(el, done) {
      const animation2 = el.animate([{}, { transform: "scale3d(0,0,0)" }], {
        duration: 1000,
      });
      animation2.onfinish = () => {
        done();
      };
      console.log("leave", el);
      done();
    },
    afterLeave(el) {
      console.log("after leave", el);
    },
  },
};
</script>

<style>
/* 1. Animating with CSS transitions */
.fade-enter-from {
  opacity: 0;
}
.fade-enter-active {
  transition: all 0.5s linear;
}
.fade-leave-to {
  transition: all 0.5s linear;
  opacity: 0;
}

/* 2. Animating with CSS animations */
h2 {
  width: 400px;
  padding: 20px;
  margin: 20px;
}

.zoom-enter-active {
  animation: zoom-in 1s linear forwards;
  transition: all 1s linear;
}

.zoom-leave-active {
  animation: zoom-out 1s linear forwards;
  transition: all 1s linear;
}

.zoom-enter-from {
  opacity: 0;
}
.zoom-leave-to {
  opacity: 0;
}
@keyframes zoom-in {
  from {
    transform: scale(0, 0);
  }
  to {
    transform: scale(1, 1);
  }
}

@keyframes zoom-out {
  from {
    transform: scale(1, 1);
  }
  to {
    transform: scale(0, 0);
  }
}
</style>
