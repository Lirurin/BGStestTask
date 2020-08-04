<template>
  <v-app id="login">
    <v-container class="login-form fill-height">
      <v-row 
        align="center"
        justify="center"
      >
        <v-col cols="12" sm="8" md="6">
          <v-card>
            <v-toolbar dark flat>
              <v-toolbar-title>Авторизация</v-toolbar-title>
            </v-toolbar>
            <v-card-text>
              <v-form ref="loginForm">
                <v-text-field
                  label="Логин"
                  name="login"
                  prepend-icon="mdi-account"
                  type="text"
                  :rules="rules.login"
                ></v-text-field>
                <v-text-field
                  id="password"
                  label="Пароль"
                  name="password"
                  prepend-icon="mdi-lock"
                  type="password"
                  :rules="rules.password"
                ></v-text-field>
              </v-form>
            </v-card-text>
            <div class="login-form__actions">
              <v-spacer></v-spacer>
              <v-btn @click ="logInAcc"
                :disabled = isLogging
              >Войти</v-btn>
            </div>
          </v-card>
        </v-col>
      </v-row>
    </v-container>
  </v-app>
</template>

<script>
export default {
  data: () => ({
    isLogging: false,
    
    rules: {
      login: [
        value => !!value || 'Обязательно',
        value => (value && value.length >= 3) || 'Минимальная длинна - 3 символа',
      ],
      password: [
        value => !!value || 'Обязательно',
        value => (value && value.length >= 3) || 'Минимальная длинна - 3 символа',
      ],
    } 
  }),

  methods: {
    logInAcc() {
      if (this.isLogging === false && this.$refs.loginForm.validate()) {
        this.getFakeData()
      }
    },

    getFakeData() {
      this.isLogging = true;

      let promise = new Promise((resolve, reject) => {
        let resolveTimer = setTimeout(() => {
          resolve( 
            {
              name: 'David',
              email: 'davidtennant@gmail.com',
              src: 'https://i.pinimg.com/736x/3a/04/4f/3a044f1b881c9276576f450dd645b4cc--dexter-crazy-man.jpg',
            }
          )
          clearTimeout(resolveTimer)
        }, 2000)
      })
      
      promise.then(data => {
        this.isLogging = false;
        this.$emit('login', data)
      })
    }
  }
}
</script>

<style>

.login {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.login-form__actions {
  display: flex;
  padding: 0 16px 16px 16px;
}

</style>