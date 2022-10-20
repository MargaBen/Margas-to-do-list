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

async function onSubmit() {
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
