<template>
  <q-dialog>
    <q-card class="q-pa-lg" :style="{ width: !$q.screen.xs ? '400px' : '90vw' }"
      ><div class="text-h5 q-pb-md row justify-between">
        <span> {{ $t("contact") }}</span> <span>(+998) 90 501-90-00</span>
      </div>
      <q-form @submit="onSubmit" @reset="onReset" class="q-gutter-md">
        <q-input
          color="green"
          filled
          v-model="name"
          :label="$t('yourname')"
          :hint="$t('namesurname')"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
        />

        <q-input
          color="green"
          filled
          v-model="companyname"
          :label="$t('companyname')"
          :hint="$t('nameyourcompany')"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
        />

        <q-input
          color="green"
          filled
          v-model="email"
          :label="$t('youremailphone')"
          :hint="$t('emailorphone')"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
        />

        <q-input
          color="green"
          filled
          v-model="question"
          type="textarea"
          :label="$t('leavemessage')"
          :hint="$t('letscooperate')"
          lazy-rules
          :rules="[(val) => (val && val.length > 0) || $t('typesomething')]"
        />

        <div>
          <q-btn outline :label="$t('submit')" type="submit" color="green" />
          <q-btn
            :label="$t('reset')"
            type="reset"
            color="primary"
            outline
            class="q-ml-sm"
          />
        </div>
      </q-form>
    </q-card>
  </q-dialog>
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
