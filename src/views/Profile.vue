<template>
  <h1>User Profile</h1>

  <p>
    User: {{ user }}
    <br />
    Token: {{ token }}
  </p>

</template>

<script>
import { useAuthStore } from "../stores/auth";
import { useRouter } from "vue-router";

export default {
  setup() {
    const { user, token } = useAuthStore();
    const router = useRouter();

    if (token == "") {
      router.replace("/login");
    }

    return {
      user,
      token,
    };
  },
};
</script>

<style></style>
