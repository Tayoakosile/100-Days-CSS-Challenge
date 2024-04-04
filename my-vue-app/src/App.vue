<script setup>
import { onMounted } from "vue";
import { gsap } from "gsap";
import TextPlugin from "gsap/TextPlugin";

gsap.registerPlugin(TextPlugin);

const tl = gsap.timeline({ defaults: { duration: 1, ease: "power3" } });
const runAnimation = () => {
  tl.to(
    "#circle",

    {
      keyframes: {
        "0%": {
          scale: 1,
        },
        "50%": {
          scale: 2,
        },
        "100%": {
          scale: 0,
        },
      },
    }
  )
    .to(
      "#lines",
      {
        duration: 1,
        keyframes: {
          "0%": {
            width: 0,
          },
          "100%": {
            width: 288,
          },
        },
      },
      ">"
    )
    .to("#line-1", {
      duration: 2,
      x: -200,
    })
    .to(
      "#line-2",
      {
        duration: 2,
        x: 200,
      },
      "<"
    )
    .to(
      "#text_container",
      {
        height: 80,
      },
      ">-1.5"
    )
    .to(
      ".animation_container",
      {
        duration: 2,
        "--collapse_container--child-width": "22px",
        ease: "back",
      },
      ">-0.5"
    )
    .to(
      "h1",
      {
        duration: 0.5,
        height: "100%",
      },
      ">-2"
    )
    .to(
      ["#mini_text-1", "#mini_text-2"],
      {
        ease: "back",
        keyframes: { x: [4, 0] },
        opacity: 1,
      },
      ">"
    );
};
onMounted(() => runAnimation());
</script>

<template>
  <div class="animation_container">
    <button class="bg-red-400 m-32 p-3" @click="runAnimation">Run Animation</button>
    <section class="frame px-4 flex items-center justify-center relative">
      <div id="circle" class="absolute w-16 h-16 bg-white rounded-full"></div>
      <ul class="relative flex justify-center w-0 h-fit overflow-x-hidden" id="lines">
        <li id="line-1" class="w-[150px] h-1 bg-white"></li>
        <li id="line-2" class="w-[150px] h-1 bg-white"></li>
      </ul>
      <ul
        class="h-0 w-[80%] border-x-4 border-white collapse_container absolute"
        id="text_container"
      >
        <p
          id="mini_text-1"
          class="absolute text-4xl tracking-wider -top-[1.75rem] uppercase right-[4rem] opacity-0"
        >
          Collect
        </p>
        <p
          id="mini_text-2"
          class="absolute text-4xl tracking-wider top-[70px] uppercase right-[2rem] opacity-0"
        >
          Not Things
        </p>

        <div
          class="w-full h-10 bg-green-500 collapse_container--child text-6xl uppercase"
        >
          <div class="flex h-[65%] relative top-3 justify-center items-center">
            <h1 class="h-0 overflow-y-hidden font-bold">
              <span>Moments</span>
            </h1>
          </div>
        </div>
      </ul>
    </section>
  </div>
</template>

<style scoped lang="scss">
.animation_container {
  --collapse_container--child-width: 0px;
  --hello_world_here: #ffffff;
}
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
.collapse_container,
.collapse_container--child {
  @apply after:h-1 after:bg-white after:block after:absolute before:h-1 before:bg-white before:block before:absolute  before:right-0;
  &::after {
    width: var(--collapse_container--child-width);
  }
  &::before {
    width: var(--collapse_container--child-width);
  }
}

.collapse_container {
  @apply after:top-0 before:top-0 before:z-[1000];
}

.collapse_container--child {
  @apply before:bottom-0 after:bottom-0  before:z-[1000] h-full;
  background-color: var(--hello_world);
}
</style>

<!-- .collapse_container,
.collapse_container--child {
  @apply after:w-4 after:h-0.5 after:bg-white after:block after:absolute  before:w-4 before:h-0.5
   before:bg-white before:block before:absolute relative  before:right-0;
} -->
