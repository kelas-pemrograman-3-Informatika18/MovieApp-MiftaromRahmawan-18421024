<template>
  <q-layout view="lHh Lpr lFf">
    <q-header class="bg-white text-blue-grey-14">
      <q-toolbar>
        <q-btn dense flat round icon="menu" @click="leftDrawerOpen = !leftDrawerOpen"/>
        <q-space></q-space>
        <q-btn round flat>
          <q-avatar>
            <img src="https://cdn.quasar.dev/img/boy-avatar.png">
          </q-avatar>
            <q-menu>
            <q-list style="min-width: 100px">
              <q-separator />
              <q-item clickable to="profile" v-close-popup>
                <q-item-section>Profile</q-item-section>
              </q-item>
              <q-separator />
              <q-item clickable v-close-popup @click="logout()">
                <q-item-section>Logout</q-item-section>
              </q-item>
            </q-list>
            </q-menu>
        </q-btn>
      </q-toolbar>
    </q-header>

    <q-drawer
      v-model="leftDrawerOpen"
      show-if-above
      bordered
      content-class="bg-primary text-white"
    >
      <q-scroll-area class="fit">
        <q-list>
        <q-item
          class="justify-center text-center q-mt-md"
          clickable active-class="active" to="profile">
            <div>
              <q-avatar size="120px">
                <img src="https://cdn.quasar.dev/img/boy-avatar.png">
              </q-avatar>
              <div class="text-weight-bold q-mt-md">{{ $q.localStorage.getItem('dataUser').namaLengkap }}</div>
              <div>Admin Aplikasi Penjualan DVD Film</div>
            </div>
        </q-item>
        <q-item clickable active-class="active" exact v-ripple :to="{ name: 'dashboardAdmin'}">
          <q-item-section avatar>
            <q-icon name="dashboard" />
          </q-item-section>

          <q-item-section>Dashboard</q-item-section>
        </q-item>
        <q-item clickable active-class="active" exact v-ripple :to="{ name: 'dataDVD'}">
          <q-item-section avatar>
            <q-icon name="theaters" />
          </q-item-section>

          <q-item-section>Data DVD</q-item-section>
        </q-item>
        <q-item clickable active-class="active" exact v-ripple :to="{ name: 'inputBarang'}">
          <q-item-section avatar>
            <q-icon name="input" />
          </q-item-section>

          <q-item-section>
            Input DVD
          </q-item-section>
        </q-item>
        <q-item clickable active-class="active" exact v-ripple :to="{ name: 'dataUser'}">
          <q-item-section avatar>
            <q-icon color="white" name="supervisor_account" />
          </q-item-section>

          <q-item-section>
            Data User
          </q-item-section>
        </q-item>
        <q-item clickable @click="logout()">
          <q-item-section avatar>
            <q-icon name="power_settings_new" />
          </q-item-section>

          <q-item-section>
            Log out
          </q-item-section>
        </q-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>

    <q-page-container class="bg-grey-4">
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
export default {
  name: 'MainLayout',
  data () {
    return {
      leftDrawerOpen: false
    }
  },
  methods: {
    logout () {
      this.$q.localStorage.remove()
      this.$router.push({ name: 'loginPage' })
    }
  }
}
</script>
<style>
.active {
  color: #F56200;
  background-color: #E0E0E0;
  padding-right: 10;
}
</style>
