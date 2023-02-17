<script setup lang="ts">
import { ref } from 'vue';
import { QPage, QForm, QInput, QBtn, useQuasar } from 'quasar';
import { supabase } from 'src/lib/supabaseClient';
import { AuthError } from '@supabase/gotrue-js';

const email = ref('');
const password = ref('');

const $q = useQuasar();

const createUser = async () => {
  if (email.value && password.value) {
    try {
      const { data, error } = await supabase.auth.signUp({
        email: email.value,
        password: password.value,
      });

      if (data.session && data.user) {
        $q.notify({
          color: 'green-4',
          message: 'Account created',
        });
      }

      if (error) {
        throw error;
      }
    } catch (e) {
      if (e instanceof AuthError) {
        $q.notify({
          message: e.message,
          color: 'red',
        });
      }
    }
  }
};
</script>

<template>
  <QPage class="row items-center justify-evenly">
    <QForm @submit="createUser()">
      <QInput
        v-model="email"
        outlined
        label="Name"
        hint="Your username"
        :rules="[val => val?.length > 0 || 'Type in a name']"
      ></QInput>
      <QInput
        class="q-mt-md"
        v-model="password"
        outlined
        label="Password"
        hint="Your password"
        :rules="[val => val?.length > 0 || 'Type in a password']"
      ></QInput>
      <QBtn class="q-mt-md" type="submit" label="Submit" color="primary"></QBtn>
    </QForm>
  </QPage>
</template>
