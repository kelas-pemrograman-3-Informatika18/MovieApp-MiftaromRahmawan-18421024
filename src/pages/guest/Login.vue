<template>
  <q-layout class="bg-brown-12" view="lHh Lpr Lff">
    <q-page-container>
      <q-page padding class="row item-center justify-center">
        <div class="row full-width">
          <div class="col-md-8 offset-md-2 col-xs-12 q-pa-md">
            <q-card flat class="text-blue-grey-14">
              <div class="row item-center">
                <div class="col-md-6 col-sm-12-col-xs-12">
                  <div class="row q-pt-xl q-pa-md">
                    <div class="col-md-11 offset-1">
                      <q-img src="statics/login.png"></q-img>
                    </div>
                  </div>
                </div>
                <div class="col-md-6">
                  <q-card-section>
                    <div class="text-h4">MovieApp</div>
                    <div>Login Akun</div>
                  </q-card-section>
                  <q-form
                    @submit="login"
                  >
                    <q-card-section>
                      <q-input v-model="username" label="Username"/>
                      <q-input v-model="password" type="password" label="Password"/>
                    </q-card-section>
                    <q-card-section>
                      <q-btn type="submit" class="full-width" unelevated color="primary" label="Login"/>
                      <q-btn :to="{ name: 'registerPage' }" class="full-width q-mt-sm" unelevated flat color="primary" label="Register"/>
                    </q-card-section>
                  </q-form>
                </div>
              </div>
            </q-card>
          </div>
        </div>
      </q-page>
    </q-page-container>
  </q-layout>
</template>
<script>
export default {
  data () {
    return {
      username: null,
      password: null
    }
  },
  methods: {
    login () {
      this.$axios.post('user/login', {
        username: this.username,
        password: this.password
      }).then(res => {
        if (res.data.sukses) {
          this.$q.localStorage.set('dataUser', res.data.data)
          if (res.data.data.level === 1) {
            this.$router.push({ name: 'dashboardAdmin' })
            this.$showNotif(res.data.pesan, 'positive')
          } else {
            this.$router.push({ name: 'homeUser' })
            this.$showNotif(res.data.pesan, 'positive')
          }
        } else {
          this.$showNotif(res.data.pesan, 'negative')
        }
      })
    }
  }
}
</script>
