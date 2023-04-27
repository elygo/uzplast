<template>
  <div class="q-pa-md" style="max-width: 400px">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
      <q-input
        color="green"
        filled
        v-model="name"
        label="Your name"
        hint="Name and surname"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
      />

      <q-input
        color="green"
        filled
        v-model="email"
        label="Your email/phone"
        hint="Email or Phone number"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
      />

      <q-input
        color="green"
        filled
        v-model="description"
        type="textarea"
        label="Message"
        hint="Description"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
      />

      <div>
        <q-btn :label="$t('submit')" type="submit" color="green" />
        <q-btn
          :label="$t('reset')"
          type="reset"
          color="red"
          flat
          class="q-ml-sm"
        />
      </div>
    </q-form>
  </div>
</template>

<script>
import axios from "axios";
import useQuasar from "quasar/src/composables/use-quasar.js";
import { ref } from "vue";
import { useI18n } from "vue-i18n";

export default {
  setup() {
    const $q = useQuasar();

    const name = ref(null);
    const email = ref(null);
    const description = ref(null);

    const { t } = useI18n();

    return {
      name,
      email,
      description,

      async onSubmit() {
        try {
          await axios.post("http://54.92.237.130:8080/contact", {
            email: email.value,
            fullName: name.value,
            description: description.value,
          });

          $q.notify({
            color: "green-4",
            textColor: "white",
            icon: "cloud_done",
            message: "Submitted",
          });
        } catch (error) {
          console.error(error);
          $q.notify({
            color: "red-5",
            textColor: "white",
            icon: "warning",
            message: "Something went wrong",
          });
        }
      },

      onReset() {
        name.value = null;
        email.value = null;
        description.value = null;
      },
    };
  },
};
</script>
