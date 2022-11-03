<script setup>
import { useQuasar } from "quasar";
import { ref } from "vue";
import { useUserStore } from "../stores/user";
import { storeToRefs } from "pinia";
import { useRouter } from "vue-router";

const $q = useQuasar();
const router = useRouter();
const userStore = useUserStore();
const { user, session } = storeToRefs(userStore);

const name = ref(null);
const email = ref(null);
const password = ref(null);
const isPwd = ref(true);
const loading = ref(false);

async function signIn() {
  if (!password.value) {
    alert("password or e-mail incorrect!");
  } else {
    try {
      loading.value = true;
      await userStore.signIn(email.value, password.value);
      router.push({ path: "/" });
    } catch {
      alert("try again... something is wrong 😢");
    } finally {
      loading.value = false;
    }
  }
}
</script>

<template>
  <div class="q-pa-md">
    <div class="q-gutter-y-md column">
      <q-form @submit="signIn" class="q-gutter signup-class">
        <q-input v-model="email" dense type="email" label="e-mail" hint="">
          <template v-slot:append> <q-icon name="mail" /> </template>
        </q-input>

        <q-input
          v-model="password"
          :dense="dense"
          :type="isPwd ? 'password' : 'text'"
          hint=""
          label="password"
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
          <q-btn label="Login" type="submit" color="primary" />
        </div>
      </q-form>
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
