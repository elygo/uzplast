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
            no-caps
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
            class="customText"
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
          :scrollAreaRefDrawer="scrollAreaRef"
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
          <div
            class="home__text"
            :style="{
              width: !$q.screen.xs && !$q.screen.sm ? '50%' : '100%',
              display: 'flex',
              flexDirection: 'column',
              justifyContent: 'center',
              gap: !$q.screen.xs && !$q.screen.sm ? '25px' : '',
              alignItems:
                !$q.screen.xs && !$q.screen.sm ? 'flex-start' : 'center',
            }"
          >
            <span class="home__text-title"
              >{{ $t("plastic") }}
              <span class="text-primary">{{ $t("profiles") }}</span>
              <div class="home__text-title--border"></div>
            </span>
            <p v-if="!$q.screen.xs && !$q.screen.sm">
              {{ $t("motto") }}
            </p>
            <ul class="home__text-list">
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("qualityprice") }}
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("coloredprofiles") }}
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("warranty") }}
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("individualwork") }}
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("freedelivery") }}
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("productionwindows") }}
              </li>
              <li>
                <q-icon
                  size="1.5rem"
                  name="check_circle"
                  color="primary"
                  class="q-mr-md"
                />{{ $t("installation") }}
              </li>
            </ul>
            <button class="home__text-btn" @click="contactDialog()">
              {{ $t("contactus") }}</button
            ><PartnerRequestForm />
          </div>
          <div class="home__content" v-if="!$q.screen.xs && !$q.screen.sm">
            <div class="home__content-image">
              <img
                :style="{ width: 'calc(80%)' }"
                src="../assets/2Elegante.png"
                alt="windows_colored"
                srcset=""
              />
            </div>
          </div>
        </div>

        <!-- products section -->
        <div class="container">
          <div
            class="q-pa-md products column"
            :style="{
              height:
                !$q.screen.xs && !$q.screen.sm ? 'calc(100vh - 82px)' : '',
            }"
          >
            <span
              class="products__title"
              :style="{
                justifyContent:
                  !$q.screen.xs && !$q.screen.sm ? 'flex-start' : 'center',
              }"
            >
              Products
            </span>
            <div
              class="row wrap"
              :style="{
                minHeight:
                  !$q.screen.xs && !$q.screen.sm ? 'calc(100% - 150px)' : '',
                justifyContent: !$q.screen.xs ? 'space-between' : 'center',
                alignItems: !$q.screen.xs && !$q.screen.sm ? '' : '',
              }"
            >
              <q-card
                v-for="product in products"
                :key="product.id"
                class="q-mb-md"
                :style="{
                  width: !$q.screen.xs ? '250px' : '90vw',
                }"
              >
                <q-img :src="product.image" style="height: 100%">
                  <div
                    class="absolute-bottom text-subtitle2 text-center bg-primary"
                  >
                    {{ product.title }}
                  </div>
                </q-img>
              </q-card>
            </div>
          </div>
        </div>

        <!-- quality section -->
        <div class="bg-primary quality">
          <div
            class="q-pa-md container"
            :style="{
              display: 'flex',
              flexDirection: 'column',
              height: 'calc(100vh - 82px)',
              width: '100%',
            }"
          >
            <span
              class="quality__title"
              :style="{
                justifyContent:
                  !$q.screen.xs && !$q.screen.sm ? 'flex-start' : 'center',
              }"
            >
              {{ $t("Quality") }}
            </span>
            <div
              :style="{
                display: 'flex',
                alignItems: 'center',
                justifyContent: 'center',
                flexDirection: !$q.screen.xs ? 'row' : 'column',
                height: 'calc(100vh - 150px)',
              }"
            >
              <div
                :style="{
                  display: 'flex',
                  flexDirection: 'column',
                  alignItems: 'center',
                  justifyContent: 'center',
                  width: !$q.screen.xs ? 'calc(50%)' : 'calc(100%)',
                  height: !$q.screen.xs ? 'calc(90%)' : 'calc(50%)',
                }"
              >
                <img
                  src="../assets/glass_in_summer.svg"
                  alt="summer"
                  :style="{
                    width: !$q.screen.xs ? 'calc(60%)' : 'calc(50%)',
                    height: !$q.screen.xs ? 'calc(100%)' : 'calc(80%)',
                  }"
                />

                <div class="col justify-center">
                  <span
                    class="text-weight-bold text-light-blue-6"
                    :style="{
                      fontSize:
                        !$q.screen.xs && !$q.screen.sm ? '34px' : '24px',
                      textAlign: 'center',
                    }"
                  >
                    SALQIN YOZ
                  </span>
                </div>
                <div
                  class="col justify-center"
                  :style="{
                    fontSize: !$q.screen.xs && !$q.screen.sm ? '24px' : '14px',
                    textAlign: 'center',
                  }"
                >
                  Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                  Facere, aliquid eligendi, blanditiis maiores explicabo
                  repellendus neque tempore officia et
                </div>
              </div>
              <div
                :style="{
                  display: 'flex',
                  flexDirection: 'column',
                  alignItems: 'center',
                  justifyContent: 'space-evenly',
                  width: !$q.screen.xs ? 'calc(50%)' : 'calc(100%)',
                  height: !$q.screen.xs ? 'calc(90%)' : 'calc(50%)',
                }"
              >
                <img
                  src="../assets/glass_in_winter.svg"
                  alt="winter"
                  :style="{
                    width: !$q.screen.xs ? 'calc(60%)' : 'calc(50%)',
                    height: !$q.screen.xs ? 'calc(100%)' : 'calc(80%)',
                  }"
                />
                <div class="col justify-center">
                  <span
                    class="text-weight-bold text-yellow-9"
                    :style="{
                      fontSize:
                        !$q.screen.xs && !$q.screen.sm ? '34px' : '24px',
                      textAlign: 'center',
                    }"
                  >
                    ISSIQ QISH
                  </span>
                </div>
                <div
                  class="col justify-center align-center"
                  :style="{
                    fontSize: !$q.screen.xs && !$q.screen.sm ? '24px' : '14px',
                    textAlign: 'center',
                  }"
                >
                  Lorem ipsum, dolor sit amet consectetur adipisicing elit.
                  Facere, aliquid eligendi, blanditiis maiores explicabo
                  repellendus neque tempore officia
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- colored profiles section -->
        <div class="colored" style="height: calc(100vh - 82px)">
          <div class="q-pa-md row container">
            <div
              :style="{
                width: !$q.screen.xs ? '40%' : '100%',
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
                    cursor: 'pointer',
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
        </div>

        <!-- parallax -->
        <!-- <div :speed="0.5" style="height: calc(100vh - 82px); max-width: 100vw">
          <q-parallax src="../assets/sky-apartment.jpg">
            <h1 class="">Basic</h1>
          </q-parallax>
        </div> -->

        <!-- services section -->
        <div class="container">
          <div
            class="services"
            :style="{
              minHeight: 'calc(100vh - 82px)',
              width:
                !$q.screen.xs && !$q.screen.sm ? 'calc(60vw)' : 'calc(90vw)',
            }"
          >
            <span
              class="services__title"
              :style="{
                justifyContent:
                  !$q.screen.xs && !$q.screen.sm ? 'flex-start' : 'center',
              }"
            >
              <span>
                {{ $t("ourservices") }}
                <div class="services__title--border"></div>
              </span>
            </span>
            <q-timeline class="" color="primary">
              <q-timeline-entry
                :title="$t('production')"
                icon="warehouse"
                color="primary"
              >
                <div
                  class="bg-grey-1 q-pa-sm"
                  :style="{
                    borderTopLeftRadius: '25px',
                    borderBottomRightRadius: '25px',
                    border: '1px solid #f11637',
                  }"
                >
                  {{ $t("productioncontent") }}
                </div>
              </q-timeline-entry>
              <q-timeline-entry :title="$t('measuring')" icon="design_services">
                <div
                  class="bg-grey-1 q-pa-sm"
                  :style="{
                    borderTopLeftRadius: '25px',
                    borderBottomRightRadius: '25px',
                    border: '1px solid #f11637',
                  }"
                >
                  {{ $t("measuringcontent") }}
                </div>
              </q-timeline-entry>
              <q-timeline-entry :title="$t('delivery')" icon="local_shipping">
                <div
                  class="bg-grey-1 q-pa-sm"
                  :style="{
                    borderTopLeftRadius: '25px',
                    borderBottomRightRadius: '25px',
                    border: '1px solid #f11637',
                  }"
                >
                  {{ $t("deliverycontent") }}
                </div>
              </q-timeline-entry>

              <q-timeline-entry
                :title="$t('installationwork')"
                icon="construction"
              >
                <div
                  class="bg-grey-1 q-pa-sm"
                  :style="{
                    borderTopLeftRadius: '25px',
                    borderBottomRightRadius: '25px',
                    border: '1px solid #f11637',
                  }"
                >
                  {{ $t("installationworkcontent") }}
                </div>
              </q-timeline-entry>
              <q-timeline-entry
                :title="$t('guaranteedservice')"
                color="green"
                icon="done_all"
              >
                <div
                  class="bg-grey-1 q-pa-sm"
                  :style="{
                    borderTopLeftRadius: '25px',
                    borderBottomRightRadius: '25px',
                    border: '1px solid green',
                  }"
                >
                  {{ $t("guaranteedservicecontent") }}
                </div>
              </q-timeline-entry>
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
            height: !$q.screen.xs ? 'calc(30vw)' : 'calc(100vh)',
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
            <p class="text-white" style="font-size: 26px; font-weight: 600">
              {{ $t("contact") }}
            </p>
            <div class="text-white" style="font-size: 18px">
              <q-icon name="phone" class="q-mr-md" /><a
                style="
                  font-size: 18px;
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
                  text-decoration: none !important;
                  color: white;
                "
                href="mailto:info@uzplast.com"
                >info@uzplast.com</a
              >
            </div>
            <div class="text-white q-my-lg" style="font-size: 18px">
              <q-icon name="location_on" /> {{ $t("address") }}
            </div>
          </div>
        </div>

        <!-- footer -->
        <div class="footer text-white">
          <div
            class="q-pa-md container"
            :style="{
              display: 'flex',
              flexDirection: !$q.screen.xs && !$q.screen.sm ? 'row' : 'column',
              justifyContent: 'space-between',
              alignItems: 'center',
              width: '100%',
              height: '100%',
            }"
          >
            <div
              :style="{
                display: 'flex',
                justifyContent:
                  !$q.screen.xs && !$q.screen.sm ? 'start' : 'center',
                alignItems: 'center',
                width: !$q.screen.xs && !$q.screen.sm ? '33%' : '100%',
                height: '100%',
              }"
            >
              © 2023 Uzplast. {{ $t("rights") }}.
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
              :style="{
                display: 'flex',
                justifyContent:
                  !$q.screen.xs && !$q.screen.sm ? 'end' : 'center',
                alignItems: 'center',
                width: !$q.screen.xs && !$q.screen.sm ? '33%' : '100%',
                height: '100%',
              }"
            >
              <q-icon name="mdi-telegram" size="lg" class="q-mx-sm" />
              <q-icon name="mdi-facebook" size="lg" class="q-mx-sm" />
              <q-icon name="mdi-youtube" size="lg" class="q-mx-sm" />
              <q-icon name="mdi-instagram" size="lg" class="q-mx-sm" />
            </div>
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

    const products = ref([
      {
        id: 1,
        title: "Product 1",
        description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
        image: "./assets/antrazit.jpg",
      },
      {
        id: 2,
        title: "Product 2",
        description:
          "Praesent non justo vel nunc ultricies vestibulum sed quis magna.",
      },
      {
        id: 3,
        title: "Product 3",
        description: "Donec dictum ipsum non volutpat convallis.",
      },
      {
        id: 4,
        title: "Product 4",
        description:
          "Maecenas eu nisi velit. Etiam fermentum velit in urna bibendum.",
      },
      {
        id: 5,
        title: "Product 5",
        description:
          "Suspendisse potenti. Pellentesque non risus sit amet sapien blandit dignissim.",
      },
      {
        id: 6,
        title: "Product 6",
        description:
          "Aliquam erat volutpat. Sed eget libero quis ipsum ultrices sagittis.",
      },
      {
        id: 7,
        title: "Product 7",
        description:
          "Nullam vel turpis nec mauris tincidunt hendrerit eget in mauris.",
      },
      {
        id: 8,
        title: "Product 8",
        description: "Fusce blandit tincidunt tellus eu eleifend.",
      },
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
        backgroundColor: "#f11637",
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
      products,
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
