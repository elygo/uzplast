<template>
  <q-layout view="hHr lpR ffr">
    <q-header reveal elevated class="bg-primary text-white q-py-md">
      <q-toolbar>
        <q-toolbar-title>Title</q-toolbar-title>

        <DrawerRight
          :rightDrawerOpen="uzunroq"
          @close="(x) => (this.uzunroq = x.uzunroq)"
        />
        <q-btn dense flat round icon="menu" @click="handleClick" />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import { ref } from "vue";
import DrawerRight from "./Drawer.vue";

export default {
  components: { DrawerRight },
  data() {
    return {
      uzunroq: false,
    };
  },
  methods: {
    handleClick() {
      this.uzunroq = true;
    },
  },
};
</script>
