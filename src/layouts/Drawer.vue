<template>
  <q-drawer v-model="drawer" side="right" overlay bordered>
    En Ru Uz
    <q-icon
      name="close"
      color="red"
      @click="$emit('close', { uzunroq: false })"
    />
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
  // computed: {
  //   normalizedSize() {
  //     return this.rightDrawerOpen;
  //   },
  // },
  watch: {
    rightDrawerOpen: function (val) {
      this.drawer = val;
    },
  },
  methods: {
    handleClose() {
      this.drawer = false;
    },
  },
};
</script>
