<template>
  <div class="q-pa-md" style="max-width: 400px">
    <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
      <q-input
        filled
        v-model="name"
        :label="$t('yourname')"
        :hint="$t('namesurname')"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
      />

      <q-input
        filled
        v-model="companyname"
        :label="$t('companyname')"
        :hint="$t('nameyourcompany')"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
      />

      <q-input
        filled
        v-model="email"
        :label="$t('youremailphone')"
        :hint="$t('emailorphone')"
        lazy-rules
        :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
      />

      <q-input
        filled
        v-model="question"
        :label="$t('leavemessage')"
        :hint="$t('letscooperate')"
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
    const companyname = ref(null);
    const email = ref(null);
    const question = ref(null);

    const { t } = useI18n();

    return {
      name,
      companyname,
      email,
      question,

      async onSubmit() {
        try {
          await axios.post("http://54.92.237.130:8080/business/partner", {
            name: name.value,
            companyName: companyname.value,
            phone: email.value,
            question: question.value,
          });

          $q.notify({
            color: "green-4",
            textColor: "white",
            icon: "cloud_done",
            message: t("submitted"),
          });
        } catch (error) {
          console.error(error);
          $q.notify({
            color: "red-5",
            textColor: "white",
            icon: "warning",
            message: t("somethingwentwrong"),
          });
        }
      },

      onReset() {
        name.value = null;
        companyname.value = null;
        email.value = null;
        question.value = null;
      },
    };
  },
};
</script>
