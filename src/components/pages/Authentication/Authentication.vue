<template>
  <h1>Auth!</h1>
</template>
<script>
  export default {}
</script>
<template>
  <div class="l-auth-container">
    <div class="l-auth">
      <v-form v-model="validLogin">
        <v-text-field label="Username"
                      v-model="credentials.login"
                      prepend-icon="account_box"
                      :rules="rules"
                      required
                      color="light-blue lighten-1">
        </v-text-field>

        <v-text-field label="Password"
                      v-model="credentials.pass"
                      prepend-icon="lock"
                      :rules="rules"
                      :append-icon="loginPasswordVisible ? 'visibility' : 'visibility_off'"
                      :append-icon-cb="() => (loginPasswordVisible = !loginPasswordVisible)"
                      :type="loginPasswordVisible ? 'text' : 'password'"
                      color="light-blue lighten-1"
                      required>
        </v-text-field>

        <v-btn flat color="light-blue lighten-1" @click.native="signUpVisible = true">Create account</v-btn>
        <v-btn color="light-blue lighten-1" @click.native="submitAuthentication()">Login</v-btn>
      </v-form>
    </div>

    <div class="l-signup" v-if="signUpVisible">
      <v-form v-model="validSignUp">
        <v-text-field label="FIO"
                      v-model="newUser.FIO"
                      prepend-icon="account_box"
                      :rules="rules"
                      required
                      color="light-blue lighten-1">
        </v-text-field>
        
        <v-text-field label="E-mail"
                      v-model="newUser.email"
                      prepend-icon="email"
                      :rules="rules"
                      required
                      color="light-blue lighten-1">
        </v-text-field>

          <v-text-field label="phone number"
                      v-model="newUser.phone"
                      prepend-icon="phone"
                      :rules="rules"
                      required
                      color="light-blue lighten-1">
        </v-text-field>

          <v-text-field label="passport"
                      v-model="newUser.passport"
                      prepend-icon="chrome_reader_mode"
                      :rules="rules"
                      required
                      color="light-blue lighten-1">
        </v-text-field>

        <v-text-field label="Password"
                      v-model="newUser.password"
                      prepend-icon="lock"
                      :rules="rules"
                      :append-icon="signUpPasswordVisible ? 'visibility' : 'visibility_off'"
                      :append-icon-cb="() => (signUpPasswordVisible = !signUpPasswordVisible)"
                      :type="signUpPasswordVisible ? 'text' : 'password'"
                      color="light-blue lighten-1"
                      required>
        </v-text-field>

        <v-btn block color="light-blue lighten-1" @click.native="submitSignUp()">Sign Up</v-btn>
      </v-form>
    </div>

    <v-snackbar timeout=6000
                bottom="bottom"
                color="red lighten-1"
                v-model="snackbar">
      {{ message }}
    </v-snackbar>
  </div>
</template>
<script>
  import Authentication from '@/components/pages/Authentication'
  export default {
    data () {
      return {
        snackbar: false,
        validLogin: false,
        validSignUp: false,

        signUpVisible: false,
        loginPasswordVisible: false,
        signUpPasswordVisible: false,
        rules: [ (value) => !!value || 'This field is required' ],
        credentials: {
          login: '',
          pass: ''
        },
        newUser: {
          fio: '',
          email: '',
          passport: '',
          phone: '',
          pass: ''
        },
        message: ''
      }
    },
    methods: {
      submitAuthentication () {
        Authentication.authenticate(this, this.credentials, '/')
      },

      submitSignUp () {
        Authentication.signup(this, this.newUser, '/')
      }
    }
  }
</script>
<style lang="scss">
  @import "./../../../assets/styles";
.l-auth {
    background-color: $background-color;
    padding: 15px;
    margin: 45px auto;
    min-width: 272px;
    max-width: 320px;
    animation: bounceIn 1s forwards ease;
  }
.l-signup {
    background-color: $background-color;
    padding: 15px;
    margin: 45px auto;
    min-width: 272px;
    max-width: 320px;
    animation: slideInFromLeft 1s forwards ease;
  }
</style>