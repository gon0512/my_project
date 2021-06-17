<template>
  <q-page padding>
    <section class="row">
      <div class="col-md-4 offset-md-4">
        <q-card class="my-card q-pa-md">
          <q-card-section class="q-gutter-sm">
            <h3>Login</h3>
          </q-card-section>

          <q-card-section class="q-gutter-md">
            <q-input rounded outlined v-model="user.email" label="Email" />
            <q-input rounded outlined type="password" v-model="user.password" label="Senha" />
          </q-card-section>

          <q-card-section class="q-gutter-md">
            <div class="q-pa-sm">
              <q-btn color="secondary" class="full-width" label="Entrar" rounded />
            </div>
          </q-card-section>

          <q-card-section class="q-gutter-md">
            <p class="text-subtitle1 text-center">Esqueci minha senha</p>
            <p class="text-subtitle1 text-center">Não tenho uma conta</p>
          </q-card-section>
        </q-card>
      </div>
    </section>
  </q-page>
</template>

<script>
export default {
  // name: 'PageName',
  data () {
    return {
      user: {
        email: '',
        password: ''
      }
    }
  }
}
</script>
