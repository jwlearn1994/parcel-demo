<template lang="pug">
  #app.container
    h3 {{ title }}
    p {{ msg }}
</template>

<script>
export default {
  data() {
    return {
      title: 'Hello Parcel Vue',
      msg: 'This is a message'
    }
  }
}
</script>

<style lang="sass">
#app
  color: red
</style>