<template>
  <q-drawer v-model="drawer" side="right" overlay bordered class="text-black">
    <div class="q-pa-md row justify-between">
      <div>
        <q-btn
          flat
          color="red"
          style="font-size: large"
          @click="handleChangeLang('uz')"
          >Uz</q-btn
        >
        <q-btn
          flat
          color="red"
          style="font-size: large"
          @click="handleChangeLang('en')"
          >En</q-btn
        >
        <q-btn
          flat
          color="red"
          style="font-size: large"
          @click="handleChangeLang('ru')"
          >Ru</q-btn
        >
      </div>
      <q-btn flat round color="red" @click="handleClose" icon="close" />
    </div>
    <div class="column">
      <q-btn flat @click="handleChangePage('/')" style="font-size: xx-large">{{
        $t("home")
      }}</q-btn>
      <q-btn
        flat
        @click="handleChangePage('/message')"
        style="font-size: xx-large"
        >{{ $t("info") }}</q-btn
      >
    </div>
  </q-drawer>
</template>

<script>
export default {
  name: "DrawerRight",
  props: {
    rightDrawerOpen: {
      type: Boolean,
    },
  },
  data() {
    return {
      drawer: false,
    };
  },
  watch: {
    rightDrawerOpen: function (val) {
      this.drawer = val;
    },
  },
  methods: {
    handleClose() {
      this.$emit("close", { closeDrawer: false });
    },
    handleChangePage(route) {
      this.handleClose();
      this.$router.push(route);
    },
    handleChangeLang(lang) {
      this.$i18n.locale = lang;
    },
  },
};
</script>
