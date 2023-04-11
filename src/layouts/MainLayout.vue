<template>
  <q-layout view="hHr lpR ffr">
    <q-header
      reveal
      elevated
      class="bg-white text-black hover:bg-red q-py-md shadow-1"
    >
      <q-toolbar class="q-pl-lg q-my">
        <img
          src="../assets/logo_uzplast.svg"
          alt="Uzplast logo"
          v-bind:width="120"
          @click="handleChangePage('/')"
          style="cursor: pointer"
        />
        <q-space />
        <q-tabs
          v-model="tab"
          shrink
          stretch
          v-if="!$q.screen.xs"
          active-color="red"
        >
          <q-tab
            name="Homepage"
            :label="$t('home')"
            @click="
              scrollToDiv(0);
              handleChangePage('/');
            "
          />
          <q-tab name="About" :label="$t('about')" @click="scrollToDiv(600)" />
          <q-tab
            name="Services"
            :label="$t('services')"
            @click="scrollToDiv(1200)"
          />
          <q-tab
            name="Products"
            :label="$t('products')"
            @click="scrollToDiv(1800)"
          />
          <q-tab
            name="Contact"
            :label="$t('contact')"
            @click="scrollToDiv(2400)"
          />
          <q-space />
        </q-tabs>

        <q-space />
        <q-select
          borderless
          label-color="red"
          v-if="!$q.screen.xs"
          v-model="selectedLanguage"
          :options="language"
          option-label="value"
          option-value="label"
          @update:model-value="handleChangeLang"
        />
        <q-space v-if="$q.screen.xs" />

        <DrawerRight
          :rightDrawerOpen="closeDrawer"
          @close="(x) => (this.closeDrawer = x.closeDrawer)"
        />
        <q-btn
          v-if="$q.screen.xs"
          dense
          flat
          round
          icon="menu"
          @click="handleClick"
        />
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
      <q-scroll-area
        :thumb-style="thumbStyle"
        ref="scrollAreaRef"
        style="height: calc(100vh - 82px); max-width: 100vw"
        @scroll="setPositionOnScroll"
      >
        <div class="q-pa-md home" style="height: 600px">home</div>
        <div class="q-pa-md about" style="height: 600px">about</div>
        <div :speed="0.5" class="parallax_container">
          <q-parallax src="../assets/sky-apartment.jpg">
            <h1 class="">Basic</h1>
          </q-parallax>
        </div>
        <div
          class="q-pa-lg services q-mx-auto"
          :style="{
            width: !$q.screen.xs ? 'calc(60vw)' : 'calc(100vw)',
          }"
        >
          <q-timeline class="q-mx-lg" color="red">
            <q-timeline-entry heading>Bizning xizmatlar</q-timeline-entry>
            <q-timeline-entry
              title="Ishlab chiqarish"
              icon="warehouse"
              color="red"
            >
              <div class="bg-grey-3 q-pa-sm rounded-borders">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
                eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                enim ad minim veniam, quis nostrud exercitation ullamco laboris
                nisi ut aliquip ex ea commodo consequat.
              </div>
            </q-timeline-entry>
            <q-timeline-entry title="O'lchov olish" icon="design_services">
              <div class="bg-grey-3 q-pa-sm rounded-borders">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
                eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                enim ad minim veniam, quis nostrud exercitation ullamco laboris
                nisi ut aliquip ex ea commodo consequat.
              </div>
            </q-timeline-entry>
            <q-timeline-entry title="Yetkazib berish" icon="local_shipping">
              <div class="bg-grey-3 q-pa-sm rounded-borders">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
                eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                enim ad minim veniam, quis nostrud exercitation ullamco laboris
                nisi ut aliquip ex ea commodo consequat.
              </div>
            </q-timeline-entry>
            <q-timeline-entry title="Montaj ishlari" icon="construction">
              <div class="bg-grey-3 q-pa-sm rounded-borders">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
                eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                enim ad minim veniam, quis nostrud exercitation ullamco laboris
                nisi ut aliquip ex ea commodo consequat.
              </div>
            </q-timeline-entry>
            <q-timeline-entry
              title="Kafolatli xizmat"
              color="green"
              icon="done_all"
            >
              <div class="bg-grey-3 q-pa-sm rounded-borders">
                Lorem ipsum dolor sit amet, consectetur adipisicing elit, sed do
                eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut
                enim ad minim veniam, quis nostrud exercitation ullamco laboris
                nisi ut aliquip ex ea commodo consequat.
              </div>
            </q-timeline-entry>
          </q-timeline>
        </div>
        <div
          class="q-mx-auto"
          :style="{
            display: 'flex',
            flexDirection: !$q.screen.xs ? 'row' : 'column',
            width: !$q.screen.xs ? 'calc(100vw)' : 'calc(100vw)',
            height: !$q.screen.xs ? 'calc(30vw)' : 'calc(80vw)',
          }"
        >
          <div
            :style="{
              width: !$q.screen.xs ? 'calc(50%)' : 'calc(100%)',
              height: 'calc(100%)',
            }"
          >
            <MapLocation />
          </div>
          <div
            class="bg-red q-pa-xl"
            :style="{
              width: !$q.screen.xs ? 'calc(50%)' : 'calc(100%)',
              height: 'calc(100%)',
            }"
          >
            <p
              class="text-white"
              style="
                font-size: 26px;
                font-family: 'Montserrat';
                font-weight: 600;
              "
            >
              {{ $t("contact") }}
            </p>
            <div
              class="text-white"
              style="font-size: 18px; font-family: 'Montserrat'"
            >
              <q-icon name="phone" class="q-mr-md" /><a
                style="
                  font-size: 18px;
                  font-family: 'Montserrat';
                  text-decoration: none !important;
                  color: white;
                "
                href="tel:+99895019000"
                >(+998) 91 501-90-00</a
              >
              <br />
              <q-icon name="email" class="q-mr-md" />
              <a
                style="
                  font-size: 18px;
                  font-family: 'Montserrat', sans-serif;
                  text-decoration: none !important;
                  color: white;
                "
                href="mailto:info@uzplast.com"
                >info@uzplast.com</a
              >
            </div>
            <div
              class="text-white q-my-lg"
              style="font-size: 18px; font-family: 'Montserrat', sans-serif"
            >
              <q-icon name="location_on" /> {{ $t("address") }}
            </div>
          </div>
        </div>
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
            <div
              class="row items-center"
              style="width: 33%; height: 100%"
            ></div>
          </div>
        </div>
      </q-scroll-area>
      <q-btn
        v-if="scrollPos > 400"
        round
        color="red"
        icon="expand_less"
        @click="scrollToDiv(0)"
        class="scroll-to-top"
      />
    </q-page-container>
  </q-layout>
</template>

<script>
import router from "src/router";
import { ref } from "vue";
import DrawerRight from "./Drawer.vue";
import MapLocation from "../components/MapLocation.vue";
import { useI18n } from "vue-i18n";
import { useRouter } from "vue-router";

export default {
  components: { DrawerRight, MapLocation },
  setup() {
    const tab = ref("Homepage");
    const isActive = ref(false);
    const closeDrawer = ref(false);
    const scrollAreaRef = ref(null);
    const scrollPos = ref(0);

    const router = useRouter();

    const { t, locale } = useI18n({ useScope: "global" });

    const selectedLanguage = ref("uz");
    const language = ref([
      { label: "O`zbekcha", value: "uz" },
      { label: "English", value: "en" },
      { label: "Русский", value: "ru" },
    ]);

    function handleClick() {
      closeDrawer.value = !closeDrawer.value;
    }

    function scrollToDiv(height) {
      scrollAreaRef.value.setScrollPosition("vertical", height, 400);
    }

    function handleChangeLang(lang) {
      locale.value = lang.value;
    }

    function setPositionOnScroll(e) {
      scrollPos.value = e.verticalPosition;
    }

    function handleChangePage(route) {
      router.push(route);
    }

    return {
      thumbStyle: {
        backgroundColor: "red",
      },
      selectedLanguage,
      language,
      tab,
      isActive,
      closeDrawer,
      scrollAreaRef,
      scrollPos,
      handleClick,
      scrollToDiv,
      handleChangeLang,
      setPositionOnScroll,
      handleChangePage,
    };
  },
};
</script>
