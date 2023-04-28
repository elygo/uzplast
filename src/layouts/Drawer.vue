<template>
  <q-drawer v-model="drawer" side="right" overlay bordered class="text-black">
    <div class="q-pa-md row justify-between bg-primary" style="height: 82px">
      <div>
        <q-btn
          class="q-mx-xs btn-drawer"
          round
          outlined
          color="primary"
          size="md"
          @click="handleChangeLang('Uz')"
          >Uz</q-btn
        >
        <q-btn
          class="q-mx-xs btn-drawer"
          round
          outlined
          color="primary"
          size="md"
          @click="handleChangeLang('En')"
          >En</q-btn
        >
        <q-btn
          class="q-mx-xs btn-drawer"
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
