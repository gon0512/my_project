<template>
  <q-card style="min-width: 350px">
    <q-card-section>
      <div class="text-h6">Olá! O que está acontecendo hoje?</div>
    </q-card-section>

    <q-card-section class="q-pt-none">
      <q-input filled autogrow dense v-model="posts.content" autofocus @keyup.enter="sendPost" />
    </q-card-section>

    <q-card-actions align="right" class="text-primary">
      <q-btn flat label="Cancelar" v-close-popup />
      <q-btn flat label="Postar" v-close-popup />
    </q-card-actions>
  </q-card>
</template>

<script>
export default {
  name: 'AddPost',
  data () {
    return {
      posts: {
        content: ''
      },
      prompt: false
    }
  },
  methods: {
    sendPost () {
      const url = 'http://localhost:3000/post/1'
      this.$axios.post(url, this.posts)
        .then(response => {
          console.log(response.data)
          this.posts.content = ''
          this.$q.notify({
            message: 'Postagem adicionada com sucessso!',
            color: 'positive',
            position: 'center'
          })
          this.$emit('listarPosts')
        })
        .catch(error => {
          console.error(`Error: ${error}`)
          this.$q.notify({
            message: 'Ocorreu um erro ao adicionar a postagem!',
            color: 'negative',
            position: 'center'
          })
        })
    }
  }
}
</script>
