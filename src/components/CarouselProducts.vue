<template>
  <Carousel
    :autoplay="2000"
    :wrap-around="true"
    v-bind="settings"
    :breakpoints="breakpoints"
  >
    <Slide v-for="product in products" :key="product">
      <div></div>
      <div class="carousel__item">{{ product.title }}</div>
    </Slide>

    <template #addons>
      <Navigation />
    </template>
  </Carousel>
</template>

<script>
import { ref, defineComponent } from "vue";
import { Carousel, Navigation, Slide } from "vue3-carousel";

import "vue3-carousel/dist/carousel.css";

export default defineComponent({
  name: "CarouselProducts",
  components: {
    Carousel,
    Slide,
    Navigation,
  },
  setup() {
    const products = ref([
      {
        id: 1,
        title: "Product 1",
        description: "Lorem ipsum dolor sit amet, consectetur adipiscing elit.",
        image: "",
      },
      {
        id: 2,
        title: "Product 2",
        description:
          "Praesent non justo vel nunc ultricies vestibulum sed quis magna.",
        image: "",
      },
      {
        id: 3,
        title: "Product 3",
        description: "Donec dictum ipsum non volutpat convallis.",
        image: "",
      },
      {
        id: 4,
        title: "Product 4",
        description:
          "Maecenas eu nisi velit. Etiam fermentum velit in urna bibendum.",
        image: "",
      },
      {
        id: 5,
        title: "Product 5",
        description:
          "Suspendisse potenti. Pellentesque non risus sit amet sapien blandit dignissim.",
        image: "",
      },
      {
        id: 6,
        title: "Product 6",
        description:
          "Aliquam erat volutpat. Sed eget libero quis ipsum ultrices sagittis.",
        image: "",
      },
      {
        id: 7,
        title: "Product 7",
        description:
          "Nullam vel turpis nec mauris tincidunt hendrerit eget in mauris.",
        image: "",
      },
      {
        id: 8,
        title: "Product 8",
        description: "Fusce blandit tincidunt tellus eu eleifend.",
        image: "",
      },
    ]);

    return {
      products,
      settings: {
        itemsToShow: 1,
        snapAlign: "center",
      },
      breakpoints: {
        800: {
          itemsToShow: 3,
          snapAlign: "center",
        },
      },
    };
  },
});
</script>

<style>
.carousel * {
  box-sizing: unset;
}
.carousel__icon {
  height: 28px;
  width: 28px;
}

.carousel__prev,
.carousel__next {
  border: 2px solid #cf1c39;
  background-color: white;
  color: black;
  width: 55px;
  height: 50px;
  border-top-left-radius: 15px;
  border-bottom-right-radius: 15px;
}

.carousel__prev:hover,
.carousel__next:hover {
  color: white;
  background-color: #cf1c39;
  border-top-left-radius: 15px;
  border-bottom-right-radius: 15px;
  cursor: pointer;
}
</style>
