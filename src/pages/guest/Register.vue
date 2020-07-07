<template>
  <q-layout view="lHh Lpr Lff">
    <q-page-container>
      <q-page padding class="bg-brown-11">
        <div class="row full-width">
          <q-card class="fixed-center col-md-4">
            <q-card-section>
              <div class="text-h4">MovieApp</div>
              <div>Halaman Registrasi</div>
            </q-card-section>
            <q-form
              @submit="onSubmit"
            >
              <q-card-section>
                <q-input
                filled
                v-model="username"
                label="Username *"
                lazy-rules
                :rules="[ val => val !== null && val.length <= 12 && val.length > 0 || 'Tolong ketik username anda max 12 karakter']"
                :dense="dense"
                />

                <q-input
                filled
                v-model="namaLengkap"
                label="Nama Lengkap *"
                lazy-rules
                :rules="[ val => val !== null && val.length > 0 || 'Tolong ketik nama lengkap anda']"
                :dense="dense"
                />

                <q-input
                  filled
                  v-model="email"
                  label="E-mail *"
                  :rules="[ val => val !== null && val.length > 0 || 'Tolong ketik email anda']"
                  :dense="dense"
                />

                <q-input
                  filled
                  type="password"
                  v-model="password"
                  label="Your password *"
                  :rules="[val => val !== null && val.length >= 6 || 'Tolong ketik passwor anda minimal 6 digit',
                  ]"
                  :dense="dense"
                />
                <div class="q-gutter-sm">
                  <q-btn type="submit" unelevated color="primary" label="Registrasi"/>
                  <q-btn :to="{ name: 'loginPage' }" unelevated flat color="primary" label="Login"/>
                </div>
              </q-card-section>
            </q-form>
          </q-card>
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
      email: null,
      password: null,
      namaLengkap: null,
      submitting: false,
      dense: true
    }
  },
  methods: {
    onSubmit () {
      this.$axios.post('user/register', {
        username: this.username,
        email: this.email,
        namaLengkap: this.namaLengkap,
        password: this.password
      }).then(res => {
        if (res.data.sukses) {
          this.$showNotif(res.data.pesan, 'positive')
          this.$router.push({ name: 'loginPage' })
        } else {
          this.$showNotif(res.data.pesan, 'negative')
        }
      })
    }
  }
}
</script>
