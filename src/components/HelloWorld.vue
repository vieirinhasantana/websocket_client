<template>
  <b-table striped hover :items="items"></b-table>
</template>
<script>
export default {
  data () {
    return {
      items: []
    }
  },
  mounted () {
    this.$options.sockets.onmessage = (wsResponse) => {
      let jsonObj = JSON.parse(wsResponse.data)
      this.items = jsonObj.payload
    }
  }
}
</script>
