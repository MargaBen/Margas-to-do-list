<script setup>
import { useQuasar } from "quasar";
import { ref } from "vue";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";
import { useRouter } from "vue-router";

const router = useRouter();
const userStore = useUserStore();
const { user, session } = storeToRefs(userStore);

const email = ref(null);
const password = ref(null);
const confirmPassword = ref(null);
const isPwd = ref(true);
const isConfirmPwd = ref(true);

async function goSignUp() {
  if (password.value !== confirmPassword.value) {
    console.log("Passwords not matching");
  } else {
    try {
      await userStore.signUp(email.value, password.value);
      if (user.value) {
        alert("please check your email for confirmation");
      }
    } catch (error) {
      console.log(error);
    }
  }
}
</script>

<template>
  <div class="q-pa-md">
    <div class="q-gutter-y-md column">
      <!-- <q-input v-model="password" filled type="password" hint="Password" /> -->
      <q-form @submit="goSignUp()" class="q-gutter signup-class" :width="550">
        <q-input
          v-model="email"
          :dense="dense"
          type="email"
          label="please enter your e-mail"
          hint=""
        />
        <q-input
          v-model="password"
          :dense="dense"
          :type="isPwd ? 'password' : 'text'"
          hint=""
          label="create password"
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>
        </q-input>

        <q-input
          v-model="confirmPassword"
          :dense="dense"
          :type="isPwd ? 'password' : 'text'"
          label="confirm password"
          hint=""
        >
          <template v-slot:append>
            <q-icon
              :name="isPwd ? 'visibility_off' : 'visibility'"
              class="cursor-pointer"
              @click="isPwd = !isPwd"
            />
          </template>
        </q-input>
        <div>
          <q-btn label="Submit" type="submit" color="primary" />
        </div>
      </q-form>
      <!-- <q-input v-model="search" filled type="search" hint="Search">
        <template v-slot:append>
          <q-icon name="search" />
        </template>
      </q-input> -->

      <!-- <q-input v-model="tel" filled type="tel" hint="Telephone number" />

      <q-input v-model="url" filled type="url" hint="URL" />

      <q-input v-model="time" filled type="time" hint="Native time" />

      <q-input v-model="date" filled type="date" hint="Native date" /> -->
    </div>
  </div>
</template>

<style scoped>
.signup-class {
  display: flex;
  flex-direction: column;
  width: 55%;
  margin: 0 22.5% 0;
}
</style>
