<template>
  <q-page class="window-height window-width row justify-center items-center">
    <div class="column">
        <div class="row">
        <q-card square class="q-pa-lg" >
        <q-img
          :src="url"
          spinner-color="white"
          style="height: 225px; max-width: 150%; border:none; background:black;"
        />
          <q-card-section>
            <q-form class="q-gutter-lg">
              <q-input class="col-12"  color="grey-3" style="border:white;" rounded outlined clearable v-model="email" type="email" label="Email" />
              <q-input class="col-12" color="grey-3" rounded outlined clearable v-model="password" type="password" label="Password" />
            </q-form>
          </q-card-section>
          <q-card-actions class="q-px-md">
            <q-btn color="primary-backgound" rounded class="full-width primary-backgound" label="Login"/>
          </q-card-actions>
          <q-card-actions class="q-px-md">
            <GoogleLogin  rounded class="full-width btn-login-google q-btn--rounded" :params="params" :onSuccess="onSuccess" :onFailure="onFailure">Login con google</GoogleLogin>
          </q-card-actions>
          <q-card-section class="text-center q-pa-none">
            <p class="text-grey-6" @click="register()">¿No esta registrado? Cree una cuenta aqui
              <q-btn rounded label="Registrarse" type="reset" color="info" flat class="q-ml-sm" />
            </p>
          </q-card-section>
        </q-card>
      </div>
    </div>
  </q-page>
</template>

<script>
import GoogleLogin from 'vue-google-login'
export default {
  name: 'Login',
  components: {
    GoogleLogin
  },
  data () {
    return {
      url: '../statics/Logo-en.png',
      // client_id is the only required property but you can add several more params, full list down bellow on the Auth api section
      params: {},
      renderParams: {
        width: 250,
        height: 50,
        longtitle: true
      },
      email: '',
      password: ''
    }
  },
  methods: {
    register () {

    },
    onFailure (googleUser) {
      console.log(googleUser, 'errror')
    },
    async onSuccess (googleUser) {
      const profile = googleUser.getBasicProfile()
      // This only gets the user information: id, name, imageUrl and email
      console.log(profile, 'profile')
    }
  },
  beforeCreate () {
    this.params = {
      client_id: '617101266164-e7d9522qt4p34j8oecltd9gmu0ktep0d.apps.googleusercontent.com'
    }
  }
}
</script>

<style>
.q-card {
  width: 100%;
}
.btn-login-google {
  background-color: red;
  color: #fff !important;
  text-align: center;
  height: 33px;
  border: none;
  border-radius: 28px;
  box-shadow: 0 1px 5px rgba(0, 0, 0, 0.2), 0 2px 2px rgba(0, 0, 0, 0.14), 0 3px 1px -2px rgba(0, 0, 0, 0.12);
}
.primary-backgound {
  background: linear-gradient(rgb(250, 217, 97), rgb(247, 107, 28));
}
</style>
