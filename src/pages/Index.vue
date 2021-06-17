<template>
  <q-page padding>
    <section class="row">
      <div class="col-md-6 offset-md-3 q-gutter-md">
        <p class="text-h5">Olá! O que está acontecendo hoje?</p>
        <q-input v-model="posts.content" filled autogrow/>
        <q-btn color="secondary" label="Postar" unelevated rounded @click="sendPost" />
        <hr>
        <section>
          <q-list bordered class="q-mb-md" v-for="allPost in allPosts" :key="allPost.id">
            <q-item>
              <q-item-section top avatar>
                <q-avatar>
                  <img src="https://cdn.quasar.dev/img/boy-avatar.png">
                </q-avatar>
              </q-item-section>

              <q-item-section>
                <q-item-label class="text-h6">{{allPost.userId}}</q-item-label>
                <q-item-label>{{allPost.content}}</q-item-label>
              </q-item-section>
            </q-item>

            <q-item>
              <div class="q-gutter-sm">
                <q-checkbox v-model="likes" label="Curtiu?" />
              </div>
            </q-item>

            <q-item-section>
              <q-item-label class="text-subtitle2 text-right q-mr-sm">Postado em: {{allPost.createdAt}}</q-item-label>
            </q-item-section>
          </q-list>
        </section>
      </div>
    </section>
    <q-dialog v-model="addPost" persistent>
      <AddPost />
    </q-dialog>
  </q-page>
</template>

<script>
import AddPost from '../components/AddPost.vue'
export default {
  name: 'PageIndex',
  components: {
    AddPost
  },
  data () {
    return {
      posts: {
        content: ''
      },
      allPosts: [],
      users: [],
      likes: false,
      addPost: true
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
    },
    listPosts () {
      const url = 'http://localhost:3000/post'
      this.$axios.get(url)
        .then(response => {
          this.allPosts = response.data
        })
        .catch(error => {
          console.error(`Error: ${error}`)
        })
    }
  },
  beforeMount () {
    this.listPosts()
  }
}
</script>
