<template>
  <q-drawer v-model="drawer" side="right" overlay bordered class="text-black">
    <div class="q-pa-md row justify-between bg-primary" style="height: 82px">
      <div>
        <q-btn
          class="q-mx-xs btn-drawer"
          no-caps
          round
          outlined
          color="primary"
          size="md"
          @click="handleChangeLang('Uz')"
          >Uz</q-btn
        >
        <q-btn
          class="q-mx-xs btn-drawer"
          no-caps
          round
          outlined
          color="primary"
          size="md"
          @click="handleChangeLang('En')"
          >En</q-btn
        >
        <q-btn
          class="q-mx-xs btn-drawer"
          no-caps
          round
          outlined
          color="primary"
          size="md"
          @click="handleChangeLang('Ru')"
          >Ru</q-btn
        >
      </div>
      <div>
        <q-btn
          class="btn-drawer"
          round
          outlined
          color="primary"
          size="md"
          @click="handleClose"
          icon="close"
        />
      </div>
    </div>
    <div class="column">
      <q-btn
        no-caps
        flat
        @click="changeScrollAreaRef(0)"
        style="font-size: x-large"
        >{{ $t("home") }}</q-btn
      >
      <q-btn
        no-caps
        flat
        @click="changeScrollAreaRef(1)"
        style="font-size: x-large"
        >{{ $t("about") }}</q-btn
      >
      <q-btn
        no-caps
        flat
        @click="changeScrollAreaRef(2)"
        style="font-size: x-large"
        >{{ $t("services") }}</q-btn
      >
      <q-btn
        no-caps
        flat
        @click="changeScrollAreaRef(3)"
        style="font-size: x-large"
        >{{ $t("products") }}</q-btn
      >
      <q-btn
        no-caps
        flat
        @click="changeScrollAreaRef(4)"
        style="font-size: x-large"
        >{{ $t("contact") }}</q-btn
      >
    </div>
  </q-drawer>
</template>

<script>
import { ref, watch } from "vue";
import { useRouter } from "vue-router";
import { useI18n } from "vue-i18n";

export default {
  name: "DrawerRight",
  props: {
    rightDrawerOpen: {
      type: Boolean,
      required: true,
    },
    scrollAreaRefDrawer: {
      type: Object,
    },
  },
  setup(props, { emit }) {
    const drawer = ref(props.rightDrawerOpen);
    const router = useRouter();
    const { t, locale } = useI18n({ useScope: "global" });

    watch(
      () => props.rightDrawerOpen,
      (val) => {
        drawer.value = val;
      }
    );

    function handleClose() {
      emit("close", { closeDrawer: false });
    }

    function handleChangePage(route) {
      handleClose();
      router.push(route);
    }

    function handleChangeLang(lang) {
      locale.value = lang;
    }

    function changeScrollAreaRef(height) {
      props.scrollAreaRefDrawer.setScrollPosition(
        "vertical",
        (window.innerHeight - 82) * height,
        400
      );
    }

    return {
      drawer,
      handleClose,
      handleChangePage,
      handleChangeLang,
      changeScrollAreaRef,
    };
  },
};
</script>
