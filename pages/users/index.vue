<template>
  <section>
    <h1>{{pageTitle}}</h1>

    <ul>
      <li v-for="user of users" :key="user.id">
        <ProjectItem :project-data="user" />
      </li>
    </ul>
  </section>
</template>

<script>

import ProjectItem from '@/components/ProjectItem.vue'

export default {
    components: {
        ProjectItem
    },
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

}
</script>

