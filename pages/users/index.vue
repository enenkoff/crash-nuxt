<template>
  <section>
    <h1>{{pageTitle}}</h1>

    <ul>
      <li v-for="user of users" :key="user.id">
        <a href="#" @click.prevent="openUser(user)">{{user.name}}</a>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
  async fetch({app, store, redirect}) {
      const token = await app.$cookies.get('quwi_user_token')
      if (!token) {
          // store.commit('removeUserToken')
          return redirect('/login')
      }

      await store.dispatch('users/fetch')

      // if (!store.state.validToken) {
      //     return redirect('/login')
      // }



    // if (store.getters['users/users'].length === 0) {
    //
    // }
  },
  data: () => ({
    pageTitle: 'Users page'
  }),
  computed: {
    users() {
      return this.$store.getters['users/users']
    }
  },
  methods: {
    openUser(user) {
      this.$router.push('/users/' + user.id)
    }
  }
}
</script>

