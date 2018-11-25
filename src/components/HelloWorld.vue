<template>
  <b-container class="bv-example-row">
    <div class="row">
      <b-table striped hover :items="items" :fields="fields"></b-table>
      <router-link to="edit">Editar valores</router-link>
    </div>
  </b-container>
</template>
<script>
export default {
  data () {
    return {
      fields: [
        {
          key: 'name',
          label: 'Nome',
          sortable: true
        },
        {
          key: 'share_value',
          label: 'Preço (R$)',
          sortable: true
        }
      ],
      items: []
    }
  },
  mounted () {
    this.socketLoad()
  },
  methods: {
    socketLoad () {
      this.$options.sockets.onmessage = (wsResponse) => {
        let jsonObj = JSON.parse(wsResponse.data)
        this.items = jsonObj.payload
      }
    }
  },
  beforeDestroy () {
    clearInterval(this.socketLoad)
  }
}
</script>
