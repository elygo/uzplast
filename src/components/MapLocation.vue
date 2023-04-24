<template>
  <GoogleMap
    api-key="AIzaSyAQRxgBbJsz_17b4vCZGytJRp2HFThf27g"
    style="height: 100%"
    :center="center"
    :zoom="14"
  >
    <InfoWindow
      :options="{
        position: center,
        content: `<p>Uzplast - PVC profiles for <br>windows & doors! </p> Website: <a href='http://www.uzplast.com'>www.uzplast.com</a> <p>Phone: <a href='tel:+998905019000'>(+998) 90 501-90-00</a> <p>`,
      }"
    />
    <Marker :options="markerOptions">
      <InfoWindow>
        <div>
          <p>Uzplast - PVC profiles for <br />windows & doors!</p>
          Website: <a href="http://www.uzplast.com">www.uzplast.com</a>

          <p>Phone: <a href="tel:+998905019000">(+998) 90 501-90-00</a></p>
        </div>
      </InfoWindow>
    </Marker>
  </GoogleMap>
</template>

<script>
import { ref, onMounted } from "vue";
import { GoogleMap, Marker, InfoWindow } from "vue3-google-map";

export default {
  name: "MapLocation",
  // eslint-disable-next-line vue/no-reserved-component-names
  components: { GoogleMap, Marker, InfoWindow },
  setup() {
    const center = { lat: 40.101679, lng: 65.34803 };
    const markerOptions = {
      position: center,
      label: "U",
      title: "Uzplast",
    };

    return { center, markerOptions };
  },
};
</script>
