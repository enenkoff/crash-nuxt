<template>
  <a href="#" @click.prevent="openUser(projectData)">{{projectData.name}}</a>
</template>

<script>


export default {
  name: 'ProjectItem',
  props: {
    projectData: {
      required: false,
      default: {}
    }
  },
    methods: {
        openUser(user) {
            this.$router.push('/users/' + user.id)
        }
    }
}

</script>
