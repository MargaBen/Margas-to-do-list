<script setup>
import Signup from "src/components/Sign-up.vue";
import Signin from "src/components/Sign-in.vue";
import { defineComponent } from "vue";
import { ref } from "vue";

const SignedUp = ref(true);
</script>

<template>
  <h1></h1>
  <Signup v-if="SignedUp" />
  <Signin v-else />
  <span v-if="SignedUp" class="signed-up-requested">
    <p>
      already signed up?

      <q-btn @click="SignedUp = !SignedUp" class="sign-up-in-button"
        >sign in</q-btn
      >
    </p>
  </span>

  <span v-else class="signed-up-requested">
    <p>
      no account?
      <q-btn @click="SignedUp = !SignedUp" class="sign-up-in-button"
        >sign up</q-btn
      >
    </p>
  </span>
</template>

<style scoped>
h1 {
  margin: 200px;
}
.sign-up-in-button {
  margin-left: 25px;
}

.signed-up-requested {
  display: flex;
  position: absolute;
  top: 84vh;
  left: 37%;
  justify-content: center;
  align-content: center;
  align-items: center;
  flex-direction: row;
}
</style>
