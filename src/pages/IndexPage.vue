<template>
  <div>
    <div
      style="
        display: flex;
        flex-direction: column;
        gap: 5px;
        position: absolute;
        right: 15px;
        top: 50vh;
        z-index: 10;
      "
    >
      <q-btn round outline color="red" size="xs" @click="scrollToDiv(400)" />
      <q-btn round outline color="red" size="xs" @click="scrollToDiv(800)" />
      <q-btn round outline color="red" size="xs" @click="scrollToDiv(1200)" />
      <q-btn round outline color="red" size="xs" @click="scrollToDiv(1600)" />
      <q-btn round outline color="red" size="xs" @click="scrollToDiv(2200)" />
    </div>

    <q-scroll-area
      :thumb-style="thumbStyle"
      ref="scrollAreaRef"
      style="height: calc(100vh - 82px); max-width: 100vw"
    >
      <div class="q-pa-md bg-yellow" style="height: 400px">our services</div>
      <div class="q-pa-md" style="height: 400px">window</div>
      <div class="q-pa-md bg-green" style="height: 400px">etc</div>
      <div class="q-pa-md" style="height: 400px">customization</div>
      <div class="q-pa-md" style="height: 400px">partners</div>
      <div class="q-pa-md" style="height: 400px">photos</div>
      <div class="q-pa-md bg-grey" style="height: 400px">Footer</div>
    </q-scroll-area>
  </div>
</template>

<script>
import { ref } from "vue";
export default {
  name: "IndexPage",
  setup() {
    const scrollAreaRef = ref(null);

    return {
      scrollAreaRef,
      thumbStyle: {
        backgroundColor: "red",
      },
      scrollToDiv(height) {
        scrollAreaRef.value.setScrollPosition("vertical", height);
      },
    };
  },
};
</script>
