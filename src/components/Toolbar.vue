<template>
  <v-toolbar fixed app>
    <v-toolbar-title>
      Филармония
    </v-toolbar-title>
    <v-spacer></v-spacer>
    <v-toolbar-items class="hidden-sm-and-down">
      <v-btn flat @click="changeLang">
        <v-img :src="flag"></v-img>
      </v-btn>
      <v-tooltip bottom>
        <v-btn flat
               @click="logout"
               slot="activator">
          {{ user.username }}
          <v-icon right>exit_to_app</v-icon>
        </v-btn>
        <span>Выйти</span>
      </v-tooltip>
    </v-toolbar-items>
  </v-toolbar>
</template>

<script>
import { mapGetters, mapActions } from 'vuex'

export default {

  name: 'Toolbar',

  computed: {
    ...mapGetters('auth', [
      'user'
    ]),
    flag () {
      return '/flag_' + this.$i18n.locale + '.png'
    }
  },

  methods: {
    ...mapActions('auth', {
      authLogout: 'logout'
    }),
    changeLang () {
      if (this.$i18n.locale === 'en') {
        this.$i18n.locale = 'ru'
      } else {
        this.$i18n.locale = 'en'
      }
    },
    logout () {
      this.authLogout().then(() => {
        this.$router.push('/login')
      })
    }
  }
}
</script>

<style scoped>

</style>
