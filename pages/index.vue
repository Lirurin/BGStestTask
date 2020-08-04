<template>
  <div>
    <LoginForm v-if="!showPage" @login="handleLoginForm"/>
    <template v-if="showPage" >
      <v-app>
        <v-container class="account">
          <v-card class="account__card">
            <v-toolbar class="account__toolbar" dark flat>
              <v-toolbar-title>Профиль пользователя</v-toolbar-title>
              <v-spacer></v-spacer>
              <span class="account__logout" @click ="logOut">&nbsp;</span> 
            </v-toolbar>
            <div class="account__card-inner">
              <img class="account__image" :src="accImgSrc" :alt="accName">
              <p class="account__text">
                <span>Имя: {{ accName }}</span>
                <span>Email: {{ accEmail }}</span>
              </p>
            </div>
          </v-card>
        </v-container>
      </v-app>
    </template>
  </div>
</template>

<script>
import LoginForm from '~/components/LoginForm.vue'

export default {
  
  components: {
    LoginForm
  },

  data: () => ({
    showPage: false,
    accName: '',
    accEmail: '',
    accImgSrc: '',
  }),

  methods: {
    handleLoginForm(value) {
      this.showPage = !this.showPage
      this.accName = value.name
      this.accEmail = value.email
      this.accImgSrc = value.src
    },
    logOut() {
      this.showPage = false;
      this.accName = '';
      this.accEmail = '';
      this.accImgSrc = '';
    }
  }
}
</script>

<style src="./index.css"/>

