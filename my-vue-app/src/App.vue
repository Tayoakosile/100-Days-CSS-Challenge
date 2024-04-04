<script setup>
import { gsap } from "gsap";
import { onMounted } from "vue";

const runAnimation = () => {
  // return;
  const tl = gsap.timeline();

  tl.to(
    "#circle",

    {
      ease: "power3",
      duration: 3,
      keyframes: {
        "0%": {
          scale: 1,
        },
        "50%": {
          scale: 2,
        },
        // "50%": {
        //   scale: 1,
        //   easeEach: "none",
        //   delay: -0.3,
        // },
        // "75%": {
        //   scale: 0.5,
        //   easeEach: "none",
        //   delay: -0.5,
        // },
        // "85%": {
        //   scale: 0.5,
        //   ease: "power3.inOut",
        // },
        "100%": {
          scale: 0.0,
        },
      },
    }
  );
  tl.to(
    "#line-1",
    {
      duration: 3,
      // reverse: true,
      keyframes: {
        "0%": {
          // transformOrigin: "top left",
          width: 0,
        },

        "25%": {
          width: 150,
          // transformOrigin: "50% 50%",
        },

        "75%": {
          width: 0,
        },
        "100%": {
          width: -150,
        },
      },
    },
    "<+=1.5"
  ).to(
    "#line-2",
    {
      duration: 1.5,
      // reverse: true,
      keyframes: {
        "0%": {
          transformOrigin: "top right",
          width: 0,
        },
        "25%": {
          width: 150,
          transformOrigin: "50% 50%",
        },

        "75%": {
          width: 0,
        },
        "100%": {
          width: -150,
        },
      },
    },
    "<"
  );
};
onMounted(() => runAnimation());
</script>

<template>
  <button class="bg-red-400 m-32 p-3" @click="runAnimation">Run Animation</button>
  <section class="frame px-4 flex items-center justify-center relative">
    <div id="circle" class="absolute w-16 h-16 bg-white rounded-full"></div>
    <ul class="relative flex justify-center w-full" id="lines">
      <li id="line-1" class="w-0 h-1 bg-blue-500"></li>
      <li id="line-2" class="w-0 h-1 bg-white ="></li>
    </ul>
  </section>
</template>

<style scoped>
.frame {
  position: absolute;
  top: 50%;
  left: 50%;
  width: 400px;
  height: 400px;
  margin-top: -200px;
  margin-left: -200px;
  border-radius: 2px;
  box-shadow: 1px 2px 10px 0px rgba(0, 0, 0, 0.3);
  overflow: hidden;
  background: #e16d6c;
  color: #fff;
  font-family: "Open Sans", Helvetica, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
