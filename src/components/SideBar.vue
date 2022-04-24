<template>
  <div>
    <v-app-bar elevation="0" color="white" >
      <v-app-bar-nav-icon @click.stop="drawer = !drawer"></v-app-bar-nav-icon>

      <v-spacer></v-spacer>

      <v-toolbar-title justify-center>Award</v-toolbar-title>

      <v-spacer></v-spacer>

      <!-- <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon>
        <v-icon>mdi-filter</v-icon>
      </v-btn> -->

      <v-btn icon to="/filter">
        <v-icon >mdi-dots-vertical</v-icon>
      </v-btn>
    </v-app-bar>

    <v-navigation-drawer v-model="drawer" absolute temporary>
                  <v-img
        :src="require('../assets/star.png')"
        class="my-3"
        contain
        height="150"
      />
      <div align="center"> <p class="font-weight-black">
     AWARDS MENU
    </p></div>
      <v-list nav dense>
        <v-list-item-group
          v-model="group"
          active-class="deep-purple--text text--accent-4"
        >
          <v-list-item>
            <v-list-item-title>    <router-link
          to="card"
          class="nav-item nav-link"
          active-class="active"
          exact
        >
          Home
        </router-link></v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>    <router-link
          to="card"
          class="nav-item nav-link"
          active-class="active"
          exact
        >
          Cards
        </router-link></v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>    <router-link
          to="card"
          class="nav-item nav-link"
          active-class="active"
          exact
        >
          Profile
        </router-link></v-list-item-title>
          </v-list-item>

          <v-list-item>
            <v-list-item-title>    <router-link
          to="login"
          class="nav-item nav-link"
          active-class="active"
          exact
        >
          Logout
        </router-link></v-list-item-title>
          </v-list-item>

        </v-list-item-group>
      </v-list>
    </v-navigation-drawer>
  </div>
</template>

<script>
export default {
  data: () => ({
    drawer: false,
    group: null
  }),

  watch: {
    group () {
      this.drawer = false
    }
  }
}
</script>
