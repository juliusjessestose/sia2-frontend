<template>
  <div class="container mt-5 w-25 border p-3">
    <label class="text-center">
      <h1>User Registration</h1>
    </label>
    <form @submit.prevent="handleSubmit">
      <div class="form-group mt-3">
        <input
          type="text" class="form-control" id="text" placeholder="First Name" v-model="user.fname"/>
      </div>
      <div class="form-group mt-3">
        <input type="text" class="form-control" id="text" placeholder="Last Name" v-model="user.lname"/>
      </div>
      <div class="form-group mt-3">
        <input type="text" class="form-control" id="text" placeholder="Mobile Number" v-model="user.mobile"/>
      </div>
      <div class="form-group mt-3">
        <input type="text" class="form-control" id="text" placeholder="Course" v-model="user.course"/>
      </div>
      <div class="form-group mt-3">
        <input type="text" class="form-control" id="text" placeholder="Year" v-model="user.year"/>
      </div>
      <div class="form-group mt-3">
        <input type="text" class="form-control" id="text" placeholder="Address" v-model="user.address"/>
      </div>
      <div class="form-group mt-3"> <input type="password" class="form-control" id="text" placeholder="Password" v-model="user.password"/>
      </div>
      <div class="form-group mt-3">
        <input type="email" class="form-control" id="text" placeholder="Email" v-model="user.email"/>
      </div>

      <button type="submit" class="btn btn-primary mt-4">Register User</button>
    </form>
  </div>
</template>

<script>
import { useAuthStore } from "../stores/auth";
import { ref } from "vue";
import { useRouter } from "vue-router";

export default {
  setup() {
    const user = ref({
      lname: "",
      fname: "",
      mobile: "",
      email: "",
      pasword: "",
      year: "",
      course: "",
      address: "",
    });
    const authStore = useAuthStore();
    const router = useRouter();

    async function handleSubmit() {
      await fetch("http://localhost:8000/api/register", {
        method: "post",
        headers: {
          Accept: "application/json",
          "Content-Type": "application/json",
        },
        body: JSON.stringify(user.value),
      })
        .then((response) => response.json())
        .then((data) => {
          if (data.status === "success") {
            authStore.saveAuth(data.user, data.token);
            console.log(data.user);
            console.log(data.token);
            router.push("/");
          }
        });
    }
    return {
      user,
      handleSubmit,
    };
  },
};
</script>

<style></style>
