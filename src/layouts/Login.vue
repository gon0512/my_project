<template>
  <q-layout view="hHh lpR fFf">

    <q-header bordered class="bg-secondary text-white">
      <q-toolbar>
        <q-toolbar-title>
          <h3 class="q-ma-md">Postick</h3>
        </q-toolbar-title>
      </q-toolbar>
    </q-header>

    <q-page-container>
      <router-view />
    </q-page-container>

  </q-layout>
</template>

<script>
export default {
  data () {
    return {
    }
  }
}
</script>
