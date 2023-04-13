<template>
  <q-scroll-area
    ref="scrollAreaRef"
    style="height: calc(100vh - 82px); max-width: 100vw"
  >
    <div class="q-pa-md" style="height: calc(100vh - 282px)">info</div>
    <div class="footer q-pa-md bg-black text-white" style="height: 200px">
      <div class="row justify-between" style="height: 100%">
        <div class="row items-center" style="width: 33%; height: 100%">
          © 2023 Uzplast. All Rights Reserved.
        </div>
        <div
          class="row items-center justify-center"
          style="width: 34%; height: 100%"
        >
          <img
            src="../assets/logo_uzplast_white.svg"
            alt="Uzplast logo"
            v-bind:width="220"
          />
        </div>
        <div class="row items-center" style="width: 33%; height: 100%"></div>
      </div>
    </div>
  </q-scroll-area>
</template>

<script>
import { ref } from "vue";
export default {
  name: "MessagePage",
  setup() {
    const scrollAreaRef = ref(null);

    return {
      scrollToDiv(height) {
        scrollAreaRef.value.setScrollPosition("vertical", height);
      },
    };
  },
};
</script>
