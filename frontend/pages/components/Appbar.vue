<template>
    <div>
        <v-card
        >
            <v-app-bar
                dark
                class = "mx-auto overflow-hidden"
            >
            <v-app-bar-nav-icon @click="drawer = true"></v-app-bar-nav-icon>

              <v-toolbar-title>{{ title }}</v-toolbar-title>
                <v-spacer></v-spacer>
              <div id="switch">
                  <v-switch
                    inset
                    v-model = "$vuetify.theme.dark"
                    class="my-auto"
                    align="center"
                  ></v-switch>
              </div>
            </v-app-bar>

        </v-card>
            <v-navigation-drawer
                v-model="drawer"
                absolute
                temporary

            >
            <v-list
                dense
                nav
            >
                <v-list-item
                    v-for="item in items"
                    :key="item.title"
                    link
                    :to="item.route"
                >
                    <v-list-item-icon>
                        <v-icon>{{ item.icon }}</v-icon>
                    </v-list-item-icon>

                    <v-list-item-content>
                        <v-list-item-title>{{ item.title }}</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>


                <v-list-item
                    link
                    @click="logout"
                >
                    <v-list-item-icon>
                        <v-icon>{{ mdiLogoutVariant }}</v-icon>
                    </v-list-item-icon>

                    <v-list-item-content>
                        <v-list-item-title>Logout</v-list-item-title>
                    </v-list-item-content>
                </v-list-item>
            </v-list>
            </v-navigation-drawer>
    </div>
</template>

<script>
import { mdiViewDashboard, mdiAccount, mdiLogoutVariant } from '@mdi/js';


export default {
  name: 'Appbar',

  props: {
        title: String
  },

  components: {

  },

  data: () => ({
      drawer: false,
      group: null,
      items: [
          { title: "Dashboard", icon: mdiViewDashboard, route: '/Dashboard' },
          { title: "Account", icon: mdiAccount, route: '/Account' },
      ],

      mdiLogoutVariant: mdiLogoutVariant,

  }),

  methods: {
      logout() {
          this.$store.commit('auth/setJwt', null);
          this.$router.push('Home');
      },

  }
}
</script>

<style lang="scss" scoped>

#switch {
    text-align: right;
}
</style>
