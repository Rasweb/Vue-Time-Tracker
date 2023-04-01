<template>
  <div>
    <div v-if="currUser">
      <h1>Welcome {{ currUser?.name }}</h1>
      <button @click="logout">Logout</button>
    </div>
    <div v-else>
      <h1>{{ loginMode ? "Login" : "Create Account" }}</h1>
      <div>
        <div>
          <input
            v-model="username"
            type="text"
            name="username"
            id="username"
            autocomplete="none"
            placeholder="Enter username"
          />
          <label for="username">Username</label>
        </div>
        <div>
          <input
            v-model="password"
            type="password"
            name="password"
            id="password"
            autocomplete="none"
            placeholder="Enter password"
          />
          <label for="password">Password</label>
        </div>
        <div v-if="loginMode">
          <div>
            <button @click="login">Login</button>
            <button @click="loginMode = false">Create Account</button>
          </div>
        </div>
        <div v-else>
          <div>
            <input
              v-model="fullName"
              type="text"
              name="fullName"
              id="fullName"
              autocomplete="none"
              placeholder="Enter Full Name"
            />
            <label for="FullName">Full Name</label>
          </div>
          <div>
            <button @click="createAccount">Save new user</button>
            <button @click="loginMode = true">Cancel</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <div>
    <NavBarComp />
  </div>
</template>

<script setup lang="ts">
import { onMounted, ref } from "vue";
import NavBarComp from "@/components/navBarComp.vue";
import PocketBase from "pocketbase";

const username = ref("");
const password = ref("");
const loginMode = ref(true);
const fullName = ref("");

let pb: any = null;
const currUser = ref();

onMounted(async () => {
  pb = new PocketBase("http://127.0.0.1:8090");
  // Check if user and stay logged in
  pb.authStore.onChange(() => {
    currUser.value = pb.authStore.model;
  }, true);
});

const logout = () => {
  // "logout" the last authenticated model
  pb.authStore.clear();
  // currUser.value = null;
};

const login = async () => {
  try {
    const authData = await pb
      .collection("users")
      .authWithPassword(username.value, password.value);

    // after the above you can also access the auth data from the authStore
    console.log(pb.authStore.isValid);
    console.log(pb.authStore.token);
    console.log(pb.authStore.model);
    // currUser.value = pb.authStore.model;
  } catch (err: any) {
    alert(err.message);
  }
};

const createAccount = async () => {
  try {
    // example create data
    const data = {
      username: username.value,
      // "email": "test@example.com",
      // "emailVisibility": true,
      password: password.value,
      passwordConfirm: password.value,
      name: fullName.value,
    };

    const record = await pb.collection("users").create(data);

    await login();
  } catch (error: any) {
    alert(error.message);
  }
};
</script>

<style scoped></style>
