<script setup lang="ts">
import { ref } from 'vue';
import { QPage, QForm, QInput } from 'quasar';

const name = ref('');
</script>

<template>
  <QPage class="row items-center justify-evenly">
    <QForm>
      <QInput
        :model-value="name"
        outlined
        label="Name"
        hint="Your username"
      ></QInput>
      <QInput
        class="q-mt-md"
        :model-value="name"
        outlined
        label="Password"
        hint="Your password"
      ></QInput>
    </QForm>
  </QPage>
</template>
