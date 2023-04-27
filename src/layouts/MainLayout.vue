<template>
  <q-layout view="hHr lpR ffr">
    <div class="header-container">
      <q-toolbar class="q-my text-white">
        <img
          src="../assets/logo_uzplast.svg"
          alt="Uzplast logo"
          v-bind:width="120"
          @click="handleChangePage('/')"
          style="cursor: pointer"
        />
        <q-space />
        <div class="tabs-container">
          <div v-if="$q.screen.xs || $q.screen.sm" class="red-bg"></div>
          <q-tabs
            v-model="tab"
            shrink
            stretch
            v-if="!$q.screen.xs && !$q.screen.sm"
            active-color="white"
          >
            <q-tab
              name="Homepage"
              :label="$t('home')"
              @click="
                scrollToDiv(0);
                handleChangePage('/');
              "
            />
            <q-tab name="About" :label="$t('about')" @click="scrollToDiv(1)" />
            <q-tab
              name="Services"
              :label="$t('services')"
              @click="scrollToDiv(2)"
            />
            <q-tab
              name="Products"
              :label="$t('products')"
              @click="scrollToDiv(3)"
            />
            <q-tab
              name="Contact"
              :label="$t('contact')"
              @click="scrollToDiv(4)"
            />
            <q-space />
          </q-tabs>
        </div>

        <q-space />
        <div class="row text-white">
          <q-select
            borderless
            color="primary"
            label-color="white"
            v-if="!$q.screen.xs && !$q.screen.sm"
            v-model="selectedLanguage.selected"
            :options="language"
            @update:model-value="handleChangeLang"
          >
            <template v-slot:option="{ itemProps, opt, index }">
              <q-item
                :key="index"
                v-ripple
                v-bind="itemProps"
                @click="handleOptionClick(opt.value, opt.image)"
              >
                <q-item-section avatar>
                  <img :src="opt.image" />
                </q-item-section>
                <q-item-section>{{ opt.label }}</q-item-section>
              </q-item>
            </template>
          </q-select>
          <img
            class="q-mx-sm"
            :src="selectedLanguage.icon"
            alt=""
            v-if="!$q.screen.xs && !$q.screen.sm"
            style="
               {
                height: 20px;
                width: 25px;
              }
            "
          />
        </div>
        <q-space v-if="$q.screen.xs" />

        <DrawerRight
          :rightDrawerOpen="closeDrawer"
          @close="(x) => (this.closeDrawer = x.closeDrawer)"
        />
        <q-btn
          v-if="$q.screen.xs || $q.screen.sm"
          dense
          flat
          round
          icon="menu"
          @click="handleClick"
        />
      </q-toolbar>
    </div>

    <q-page-container>
      <router-view />
      <q-scroll-area
        :thumb-style="thumbStyle"
        ref="scrollAreaRef"
        style="height: calc(100vh - 82px); max-width: 100vw"
        @scroll="setPositionOnScroll"
      >
        <!-- home section -->
        <div class="q-pa-md home container" style="height: calc(100vh - 82px)">
          <div class="home__text">
            <span class="home__text-title"
              >Plastik <span class="text-primary">profillar</span></span
            >
            <p>
              Lorem ipsum dolor sit amet, consectetur adipisicing elit.
              Reprehenderit nemo aut assumenda placeat dolores dignissimos, fuga
              voluptatibus quas architecto est! Veniam commodi neque, eius atque
              beatae similique repudiandae magnam expedita.
            </p>
            <ul class="home__text-list">
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />
                Sifatli va hamyonbop plastik profillar ishlab chiqarish;
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />
                Didingizga mos ranglar, istalgan o'lchamlar;
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />30 yillik kafolat;
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />Xaridor bilan individual ishlash;
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />Hudud bo'yicha bepul yetkazib berish;
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />Deraza va eshiklar ishlab chiqarish;
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />Vaqtida va sifatli o'rnatish.
              </li>
            </ul>
            <button class="home__text-btn" @click="contactDialog()">
              Bizga yozing!
            </button>
          </div>
          <div class="home__content">
            <div class="home__content-image">
              <img
                :style="{ width: 'calc(100%)' }"
                src="../assets/2Elegante.png"
                alt="windows_colored"
                srcset=""
              />
            </div>
          </div>
        </div>

        <div class="q-pa-md about" style="height: calc(100vh - 82px)">
          <PartnerRequestForm />
        </div>

        <!-- quality section -->
        <div
          class="q-pa-md quality bg-grey-1"
          :style="{
            display: 'flex',
            flexDirection: !$q.screen.xs ? 'row' : 'column',
            height: 'calc(100vh - 82px)',
            width: '100vw',
          }"
        >
          <div
            :style="{
              display: 'flex',
              flexDirection: 'column',
              alignItems: 'center',
              width: !$q.screen.xs ? 'calc(50vw)' : 'calc(100vw)',
              height: !$q.screen.xs ? 'calc(70%)' : 'calc(50%)',
            }"
          >
            <div class="col justify-center text-h4">
              <p class="text-weight-bold text-light-blue-6">SALQIN YOZ</p>
            </div>
            <img
              src="../assets/glass_in_summer.svg"
              alt="summer"
              :style="{
                width: !$q.screen.xs ? 'calc(100%)' : 'calc(80%)',
                height: !$q.screen.xs ? 'calc(100%)' : 'calc(80%)',
              }"
            />
          </div>
          <div
            :style="{
              display: 'flex',
              flexDirection: 'column',
              alignItems: 'center',
              width: !$q.screen.xs ? 'calc(50vw)' : 'calc(100vw)',
              height: !$q.screen.xs ? 'calc(70%)' : 'calc(50%)',
            }"
          >
            <div class="col justify-center text-h4">
              <p class="text-weight-bold text-deep-orange-6">ISSIQ QISH</p>
            </div>
            <img
              src="../assets/glass_in_winter.svg"
              alt="winter"
              :style="{
                width: !$q.screen.xs ? 'calc(100%)' : 'calc(80%)',
                height: !$q.screen.xs ? 'calc(100%)' : 'calc(80%)',
              }"
            />
          </div>
        </div>

        <!-- colored profiles section -->
        <div class="q-pa-md colored row" style="height: calc(100vh - 82px)">
          <div
            :style="{
              width: !$q.screen.xs ? '30%' : '100%',
              height: !$q.screen.xs ? '600px' : '200px',
            }"
            class="row justify-center items-center"
          >
            <div
              class="q-ma-md text-center"
              v-for="(image, index) in laminatedProfiles"
              :key="index"
            >
              <div
                class="rounded-lamination-picker shadow-2 q-pa-md"
                :style="{
                  height: '60px',
                  width: '60px',
                  backgroundImage: 'url(' + image.lamination + ')',
                }"
                @click="selectedImageIndex = index"
              ></div>

              <div class="text q-mt-md">
                {{ image.alt }}
              </div>
            </div>
          </div>
          <div
            class="image-container row q-mx-auto q-my-auto"
            :style="{
              width: !$q.screen.xs ? '600px' : '90vw',
              height: !$q.screen.xs ? '400px' : '60vw',
            }"
          >
            <img
              v-for="(image, index) in selectedLaminatedProfiles"
              :key="index"
              :src="image.src"
              :alt="image.alt"
            />
          </div>
        </div>

        <!-- parallax -->
        <div :speed="0.5" style="height: calc(100vh - 82px); max-width: 100vw">
          <q-parallax src="../assets/sky-apartment.jpg">
            <h1 class="">Basic</h1>
          </q-parallax>
        </div>

        <!-- services section -->
        <div class="services">
          <div
            class="q-mx-auto"
            :style="{
              height: 'calc(100vh - 82px)',
              width: !$q.screen.xs
                ? $q.screen.sm
                  ? 'calc(80vw)'
                  : 'calc(60vw)'
                : 'calc(90vw)',
            }"
          >
            <q-timeline class="q-mx-lg" color="primary">
              <q-timeline-entry heading class="q-mt-lg" style="height: 60px">
                <transition
                  appear
                  enter-active-class="animated fadeInDown"
                  leave-active-class="animated fadeOutDown"
                  ><span v-if="scrollPos > 2200">Bizning xizmatlar</span>
                </transition>
              </q-timeline-entry>
              <transition
                appear
                enter-active-class="animated fadeInDown"
                leave-active-class="animated fadeOutDown"
              >
                <q-timeline-entry
                  title="Ishlab chiqarish"
                  icon="warehouse"
                  color="primary"
                  v-if="scrollPos > 2300"
                >
                  <div class="bg-grey-3 q-pa-sm rounded-borders">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                    sed do eiusmod tempor incididunt ut labore et dolore magna
                    aliqua. Ut enim ad minim veniam, quis nostrud exercitation
                    ullamco laboris nisi ut aliquip ex ea commodo consequat.
                  </div>
                </q-timeline-entry>
              </transition>
              <transition
                appear
                enter-active-class="animated fadeInDown"
                leave-active-class="animated fadeOutDown"
              >
                <q-timeline-entry
                  title="O'lchov olish"
                  icon="design_services"
                  v-if="scrollPos > 2400"
                >
                  <div class="bg-grey-3 q-pa-sm rounded-borders">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                    sed do eiusmod tempor incididunt ut labore et dolore magna
                    aliqua. Ut enim ad minim veniam, quis nostrud exercitation
                    ullamco laboris nisi ut aliquip ex ea commodo consequat.
                  </div>
                </q-timeline-entry>
              </transition>
              <transition
                appear
                enter-active-class="animated fadeInDown"
                leave-active-class="animated fadeOutDown"
              >
                <q-timeline-entry
                  title="Yetkazib berish"
                  icon="local_shipping"
                  v-if="scrollPos > 2500"
                >
                  <div class="bg-grey-3 q-pa-sm rounded-borders">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                    sed do eiusmod tempor incididunt ut labore et dolore magna
                    aliqua. Ut enim ad minim veniam, quis nostrud exercitation
                    ullamco laboris nisi ut aliquip ex ea commodo consequat.
                  </div>
                </q-timeline-entry>
              </transition>

              <transition
                appear
                enter-active-class="animated fadeInDown"
                leave-active-class="animated fadeOutDown"
              >
                <q-timeline-entry
                  title="Montaj ishlari"
                  icon="construction"
                  v-if="scrollPos > 2600"
                >
                  <div class="bg-grey-3 q-pa-sm rounded-borders">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                    sed do eiusmod tempor incididunt ut labore et dolore magna
                    aliqua. Ut enim ad minim veniam, quis nostrud exercitation
                    ullamco laboris nisi ut aliquip ex ea commodo consequat.
                  </div>
                </q-timeline-entry>
              </transition>
              <transition
                appear
                enter-active-class="animated fadeInDown"
                leave-active-class="animated fadeOutDown"
              >
                <q-timeline-entry
                  title="Kafolatli xizmat"
                  color="green"
                  icon="done_all"
                  v-if="scrollPos > 2700"
                >
                  <div class="bg-grey-3 q-pa-sm rounded-borders">
                    Lorem ipsum dolor sit amet, consectetur adipisicing elit,
                    sed do eiusmod tempor incididunt ut labore et dolore magna
                    aliqua. Ut enim ad minim veniam, quis nostrud exercitation
                    ullamco laboris nisi ut aliquip ex ea commodo consequat.
                  </div>
                </q-timeline-entry>
              </transition>
            </q-timeline>
          </div>
        </div>

        <!-- contact section -->
        <div
          class=""
          :style="{
            display: 'flex',
            flexDirection: !$q.screen.xs ? 'row' : 'column',
            width: !$q.screen.xs ? 'calc(100vw)' : 'calc(100vw)',
            height: !$q.screen.xs ? 'calc(30vw)' : 'calc(100vw)',
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
            class="bg-primary q-pa-lg"
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
                  font-family: 'Montserrat';
                  text-decoration: none !important;
                  color: white;
                "
                href="mailto:info@uzplast.com"
                >info@uzplast.com</a
              >
            </div>
            <div
              class="text-white q-my-lg"
              style="font-size: 18px; font-family: 'Montserrat'"
            >
              <q-icon name="location_on" /> {{ $t("address") }}
            </div>
          </div>
        </div>

        <!-- footer -->
        <div
          class="footer bg-black text-white"
          style="height: 200px; width: 100vw"
        >
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
        color="primary"
        icon="expand_less"
        @click="scrollToDiv(0)"
        class="scroll-to-top"
      />
    </q-page-container>
  </q-layout>
</template>

<script>
import router from "src/router";
import { ref, computed } from "vue";
import DrawerRight from "./Drawer.vue";
import MapLocation from "../components/MapLocation.vue";
import PartnerRequestForm from "src/components/PartnerRequestForm.vue";
import { useI18n } from "vue-i18n";
import { useRouter } from "vue-router";
import { useQuasar } from "quasar";

export default {
  components: { DrawerRight, MapLocation, PartnerRequestForm },
  setup() {
    const $q = useQuasar();
    const tab = ref("Homepage");
    const isActive = ref(false);
    const closeDrawer = ref(false);
    const scrollAreaRef = ref(null);
    const scrollPos = ref(0);
    const selectedImageIndex = ref(0);
    const laminatedProfiles = ref([
      {
        src: "./assets/window_white.jpg",
        alt: "White",
        lamination: "",
      },
      {
        src: "./assets/window_antrazit.jpg",
        alt: "Anthracite",
        lamination: "./assets/antrazit.jpg",
      },
      {
        src: "./assets/window_dub.jpg",
        alt: "Oak",
        lamination: "./assets/dub.jpg",
      },
      {
        src: "./assets/light-oak.jpg",
        alt: "Natural Oak",
        lamination: "./assets/natural_dub.jpg",
      },
    ]);

    const selectedLaminatedProfiles = computed(() => {
      return laminatedProfiles.value.filter(
        (image, index) => index === selectedImageIndex.value
      );
    });

    const router = useRouter();

    const { t, locale } = useI18n({ useScope: "global" });

    const selectedLanguage = ref({ selected: "Uz", icon: "./assets/uz.svg" });
    const language = ref([
      { label: "O`zbekcha", value: "Uz", image: "./assets/uz.svg" },
      { label: "English", value: "En", image: "./assets/gb.svg" },
      { label: "Русский", value: "Ru", image: "./assets/ru.svg" },
    ]);

    function handleClick() {
      closeDrawer.value = !closeDrawer.value;
    }

    function scrollToDiv(height) {
      scrollAreaRef.value.setScrollPosition(
        "vertical",
        (window.innerHeight - 82) * height,
        400
      );
    }

    function handleChangeLang(newValue) {
      locale.value = newValue.value;
    }

    function handleOptionClick(selectedVal, icon) {
      selectedLanguage.value.selected = selectedVal;
      selectedLanguage.value.icon = icon;
    }

    function setPositionOnScroll(e) {
      scrollPos.value = e.verticalPosition;
    }

    function handleChangePage(route) {
      router.push(route);
    }

    function contactDialog() {
      $q.dialog({
        component: PartnerRequestForm,
      });
    }

    return {
      thumbStyle: {
        backgroundColor: "#cf1c39",
      },
      selectedLanguage,
      language,
      tab,
      isActive,
      closeDrawer,
      scrollAreaRef,
      scrollPos,
      selectedImageIndex,
      laminatedProfiles,
      selectedLaminatedProfiles,
      handleClick,
      scrollToDiv,
      handleChangeLang,
      handleOptionClick,
      setPositionOnScroll,
      handleChangePage,
      contactDialog,
    };
  },
};
</script>
