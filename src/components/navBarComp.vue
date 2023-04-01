<script lang="ts">
import { RouterLink, RouterView } from "vue-router";

export default {
  data() {
    return {
      drawer: true,
      // items: [
      //   { title: "Home", icon: "mdi-home-city", to: "/" },
      //   { title: "My Account", icon: "mdi-account", to: "/tracker" },
      //   { title: "Users", icon: "mdi-account-group-outline" },
      // ],
      rail: true,
    };
  },
};
</script>
<template>
  <v-card>
    <v-layout>
      <v-navigation-drawer
        v-model="drawer"
        :rail="rail"
        permanent
        theme="dark"
        @click="rail = false"
      >
        <v-list-item
          prepend-avatar="https://randomuser.me/api/portraits/men/85.jpg"
          title="John Leider"
          nav
        >
          <template v-slot:append>
            <v-btn
              variant="text"
              icon="mdi-chevron-left"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>
        </v-list-item>

        <v-divider></v-divider>

        <v-list density="compact" nav>
          <v-list-item prepend-icon="mdi-home" title="Home" value="home" to="/">
          </v-list-item>

          <v-list-item
            prepend-icon="mdi-timelapse"
            title="Tracker"
            value="tracker"
            to="/tracker"
          ></v-list-item>
          <v-list-item
            prepend-icon="mdi-account-group-outline"
            title="About"
            value="about"
            to="/about"
          >
          </v-list-item>

          <!-- <router-link to="/about">
                <v-icon icon="mdi-account-group"></v-icon>
                ss</router-link
              > -->
        </v-list>
      </v-navigation-drawer>
    </v-layout>
  </v-card>
  <RouterView />
  <!-- <div>
    <v-card>
      <v-layout>
 
        <v-app-bar color="primary" prominent>
          <v-app-bar-nav-icon
            variant="text"
            @click.stop="drawer = !drawer"
          ></v-app-bar-nav-icon>

          <v-tabs v-model="drawer">
            <v-tab :items="items"></v-tab>
            <v-tab>s</v-tab>
          </v-tabs>

          <v-spacer></v-spacer>

          <v-btn variant="text" icon="mdi-magnify"></v-btn>

          <v-btn variant="text" icon="mdi-filter"></v-btn>

          <v-btn variant="text" icon="mdi-dots-vertical"></v-btn>
        </v-app-bar>

        <v-navigation-drawer v-model="drawer" location="top" temporary>
          <v-list :items="items"></v-list>
        </v-navigation-drawer>


      </v-layout>
    </v-card>
    <RouterView />
  </div> -->
  <!-- <header>
    <img
      alt="Vue logo"
      class="logo"
      src="@/assets/logo.svg"
      width="125"
      height="125"
    />

    <div class="wrapper">
      <nav>
        <RouterLink to="/">Home</RouterLink>
        <RouterLink to="/tracker">Tracker</RouterLink>
        <RouterLink to="/about">About</RouterLink>
      </nav>
    </div>
  </header>
  <RouterView /> -->
</template>
<style scoped>
header {
  line-height: 1.5;
  max-height: 100vh;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

nav {
  width: 100%;
  font-size: 12px;
  text-align: center;
  margin-top: 2rem;
}

nav a.router-link-exact-active {
  color: var(--color-text);
}

nav a.router-link-exact-active:hover {
  background-color: transparent;
}

nav a {
  display: inline-block;
  padding: 0 1rem;
  border-left: 1px solid var(--color-border);
}

nav a:first-of-type {
  border: 0;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

  nav {
    text-align: left;
    margin-left: -1rem;
    font-size: 1rem;

    padding: 1rem 0;
    margin-top: 1rem;
  }
}
</style>
