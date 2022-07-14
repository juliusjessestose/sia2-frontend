<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark custom ">
    <div class="container">
      <router-link to="/" class="navbar-brand hover-links">Authentication</router-link
      >
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav ms-auto">
          <li class="nav-item" v-if="token != ''">
            <router-link to="/" class="nav-link hover-links">Home</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/shouts" class="nav-link hover-links" v-if="token != ''">Shouts</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/profile" class="nav-link hover-links" v-if="token != ''">Profile</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/login" class="nav-link hover-links" v-if="token == ''">Login</router-link>
          </li>
          <li class="nav-item">
            <router-link to="/register" class="nav-link hover-links" v-if="token == ''">Register</router-link>
          </li>
          <li class="nav-item" v-if="token != ''">
            <a href="#" @click="logout" class="nav-link hover-links">Logout</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>
</template>

<script>
import { useAuthStore } from "../stores/auth";
import { useRouter } from "vue-router";
import { storeToRefs } from "pinia";
export default {
  setup() {
    const authStore = useAuthStore();
    const router = useRouter();

    const { token } = storeToRefs(useAuthStore());

    async function logout() {
      await fetch("http://localhost:8000/api/logout", {
        method: "post",
        headers: {
          Accept: "application/json",
          Authorization: "Bearer " + authStore.token,
        },
      })
        .then((response) => response.json())
        .then((data) => {
          if (data.status === "success") {
            authStore.destroy();
            router.push("/login");
          }
        });
    }

    return {
      logout,
      token,
    };
  },
};
</script>