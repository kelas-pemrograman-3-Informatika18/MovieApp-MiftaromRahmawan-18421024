<template>
  <q-layout view="lHh LpR lFf">
    <q-toolbar unelevated style="height: 50px;" class="bg-white text-blue-grey-14">
      <!-- <q-btn dense flat round icon="menu" @click="leftDrawerOpen = !leftDrawerOpen"/> -->
      <div class="text-h6 q-ml-lg">Movie App</div>
      <q-space/>
      <div v-if="$q.screen.md || $q.screen.md || $q.screen.lg || $q.screen.xl">
        <q-btn size="medium" :to="{ name: 'homeUser' }" flat>Home</q-btn>
        <q-btn size="medium" :to="{ name: 'myOrder' }" flat>Pesanan Saya</q-btn>
        <q-btn size="medium" flat>Tentang</q-btn>
        <q-btn size="medium" flat @click="logout()">Logout</q-btn>
      </div>
      <q-btn size="medium" round icon="shopping_cart" :to="{ name: 'myOrder' }" flat></q-btn>
      <q-btn flat @click="drawer = !drawer" round v-if="$q.screen.xs || $q.screen.sm" icon="menu"></q-btn>
    </q-toolbar>
    <q-drawer v-model="drawer" :width="200" :breakpoint="500" side="right">
      <q-scroll-area class="fit">
        <q-list>
          <q-btn round flat icon="keyboard_arrow_right" @click="drawer = !drawer"></q-btn>
          <q-item v-ripple clickable :to="{ name: 'homeUser' }">
            <q-item-section avatar>
              <q-icon name="home"/>
            </q-item-section>
            <q-item-section>
              Home
            </q-item-section>
          </q-item>
          <q-item v-ripple clickable>
            <q-item-section avatar>
              <q-icon name="info"/>
            </q-item-section>
            <q-item-section>
              Tentang
            </q-item-section>
          </q-item>
          <q-item v-ripple clickable @click="logout()">
            <q-item-section avatar>
              <q-icon name="power_settings_new"/>
            </q-item-section>
            <q-item-section>
              Logout
            </q-item-section>
          </q-item>
        </q-list>
      </q-scroll-area>
    </q-drawer>
    <q-page-container class="bg-grey-4">
      <router-view></router-view>
    </q-page-container>
  </q-layout>
</template>
<script>
export default {
  data () {
    return {
      drawer: false
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
