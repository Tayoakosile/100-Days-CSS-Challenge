<template>
  
  <section>
    <div
      class="relative w-[500px] h-[500px] mx-72 my-32 overflow-x-hidden"
      id="container"
    >
      <ul
        class="w-full h-full bg-white rounded-md flex justify-center items-center space-x-3 relative"
      >
        <div
          class="bg-white rounded-full w-12 h-12 absolute right-72 z-[9999]"
          id="selector"
        ></div>
        <li v-for="button in buttons" :key="button.id" class="z-[9999]">
          <button class="circle" @click="() => handleClick(button.id)">
            <!-- <div
          v-if="chosen_button.id == button.id"
          class="bg-white w-full h-full rounded-full"
        ></div> -->
          </button>
        </li>
      </ul>
      <ul
        id="box"
        class="w-[1500px] h-[500px] m-24 flex z-0 absolute -top-24 -left-24"
      >
        <li class="w-[500px] h-full bg-[#9B59B6]"></li>
        <li class="w-[500px] h-full bg-[#3498DB]"></li>
        <li class="w-[500px] h-full bg-[#1ABC9C]"></li>
      </ul>
    </div>
  </section>
  
</template>

<!-- COLORS
    1. #9B59B6
    2. #3498DB
    3. #1ABC9C
 -->

<script setup>
  import _ from "lodash";
  import { gsap } from "gsap";
  import { onMounted, ref } from "vue";

  const buttons = ref([
    {
      id: 1,
      checked: false,
      color: "#9B59B6",
    },

    {
      id: 2,
      checked: false,
      color: "#3498DB",
    },
    {
      id: 3,
      checked: false,
      color: "#1ABC9C",
    },
  ]);

  const chosen_button = ref({
    id: 1,
    checked: false,
    color: "#9B59B6",
  });

  const handleClick = (id) => {
    const buttonClickedOn = _.find(buttons.value, { id });
    chosen_button.value = buttonClickedOn;

    const timeline = gsap.timeline();

    timeline
      .to("#selector", {
        x: buttonClickedOn.id == 1 ? 0 : buttonClickedOn.id == 2 ? 68 : 136,
        ease: "back.out",
        duration: 0.6,
      })
      .to(
        "#box",
        {
          duration: 0.6,
          x:
            buttonClickedOn.id == 1
              ? 0
              : buttonClickedOn.id == 2
              ? -500
              : -1000,
          ease: "power1.out",
        },
        "<"
      );
  };

  onMounted(() => {
    const tl = gsap.timeline();
    tl.fromTo(
      "#container",
      { scale: 0.1, opacity: 0 },
      { scale: 1, opacity: 1, duration: 1, ease: "back" }
    )
      .fromTo(
        "button",
        {
          opacity: 0,
        },
        {
          opacity: 1,
          stagger: 0.2,
          ease: "back",
        },
        ">-0.5"
      )
      .fromTo(
        "#selector",
        {
          opacity: 0,
          scale: 0.2,
          ease: "back",
        },
        {
          opacity: 1,
          scale: 1,
          ease: "back",
        },
        ">-0.06"
        // "=-0.05"
      );
  });
</script>

<style lang="css" scoped>
  .circle {
    @apply w-14 h-14 rounded-full border-[1.5px] border-white p-1 active:scale-90 transition-all opacity-0;
  }

  .frame {
    position: absolute;
    top: 50%;
    left: 50%;
    background: #5e6472;
    height: 400px;
    width: 400px;
    margin-top: -200px;
    margin-left: -200px;
    border-radius: 5px;
    box-shadow: 4px 8px 16px rgba(0, 0, 0, 0.5);
    overflow: hidden;
  }
</style>
